<script lang="ts">
	export interface QuizQuestion {
		id: string;
		question: string;
		options: string[];
		correctAnswer: number;
		explanation: string;
	}

	export interface QuizData {
		topicId: string;
		topicTitle: string;
		version: string;
		questions: QuizQuestion[];
	}

	export let questions: QuizData;

	const totalQuestions = questions.questions.length;

	let currentIndex = 0;
	let selectedIndex: number | null = null;
	let answered = false;
	let score = 0;
	let completed = false;

	$: currentQuestion = questions.questions[currentIndex];
	$: isCorrect = answered && selectedIndex === currentQuestion.correctAnswer;

	function handleSelect(optionIndex: number) {
		if (answered || optionIndex < 0 || optionIndex >= currentQuestion.options.length) {
			return;
		}

		selectedIndex = optionIndex;
		answered = true;

		if (optionIndex === currentQuestion.correctAnswer) {
			score += 1;
		}
	}

	function goToNext() {
		if (!answered) return;

		if (currentIndex === totalQuestions - 1) {
			completed = true;
			return;
		}

		currentIndex += 1;
		resetQuestionState();
	}

	function resetQuestionState() {
		selectedIndex = null;
		answered = false;
	}

	function retryQuiz() {
		currentIndex = 0;
		selectedIndex = null;
		answered = false;
		score = 0;
		completed = false;
	}

	function optionClasses(index: number): string {
		const base =
			'w-full text-left px-4 py-3 border rounded-lg transition-colors duration-150 focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-400';

		if (!answered) {
			return `${base} border-gray-200 bg-white hover:border-indigo-400 hover:bg-indigo-50`;
		}

		if (index === currentQuestion.correctAnswer) {
			return `${base} border-green-500 bg-green-50 text-green-800`;
		}

		if (index === selectedIndex) {
			return `${base} border-red-500 bg-red-50 text-red-800`;
		}

		return `${base} border-gray-200 bg-white opacity-70`;
	}
</script>

{#if completed}
	<section class="mt-6 w-full max-w-2xl rounded-xl border border-gray-200 bg-white p-6 shadow-sm">
		<h2 class="text-2xl font-semibold text-gray-900">Quiz Complete</h2>
		<p class="mt-2 text-gray-700">
			You scored <span class="font-semibold text-indigo-600">{score}</span> out of
			<span class="font-semibold text-indigo-600">{totalQuestions}</span>.
		</p>
		<button
			class="mt-6 inline-flex items-center justify-center rounded-lg bg-indigo-600 px-5 py-2 text-sm font-semibold text-white shadow transition hover:bg-indigo-700 focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-400"
			type="button"
			on:click={retryQuiz}
		>
			Retry Quiz
		</button>
	</section>
{:else}
	<section class="mt-6 w-full max-w-2xl rounded-xl border border-gray-200 bg-white p-6 shadow-sm">
		<header class="mb-4 flex items-center justify-between">
			<div>
				<h2 class="text-lg font-semibold text-gray-900">{questions.topicTitle} Practice Quiz</h2>
				<p class="text-sm text-gray-500">
					Question {currentIndex + 1} of {totalQuestions}
				</p>
			</div>
			<div class="text-sm font-medium text-indigo-600">
				Score: {score} / {totalQuestions}
			</div>
		</header>

		<div>
			<p class="text-lg font-medium text-gray-900">{currentQuestion.question}</p>

			<div class="mt-4 space-y-3">
				{#each currentQuestion.options as option, index (index)}
					<button
						type="button"
						class={optionClasses(index)}
						on:click={() => handleSelect(index)}
						disabled={answered}
					>
						<span class="font-medium text-gray-900">{String.fromCharCode(65 + index)}.</span>
						<span class="ml-2 text-gray-800">{option}</span>
					</button>
				{/each}
			</div>
		</div>

		{#if answered}
			<div class="mt-5 rounded-lg border border-gray-200 bg-gray-50 p-4">
				<p class="text-sm font-semibold {isCorrect ? 'text-green-700' : 'text-red-700'}">
					{isCorrect ? 'Correct!' : 'Not quite.'}
				</p>
				<p class="mt-2 text-sm text-gray-700">{currentQuestion.explanation}</p>
			</div>
		{/if}

		<div class="mt-6 flex justify-end">
			<button
				type="button"
				class="inline-flex items-center justify-center rounded-lg bg-indigo-600 px-5 py-2 text-sm font-semibold text-white shadow transition hover:bg-indigo-700 focus:outline-none focus-visible:ring-2 focus-visible:ring-indigo-400 disabled:cursor-not-allowed disabled:bg-indigo-300"
				on:click={goToNext}
				disabled={!answered}
			>
				{currentIndex === totalQuestions - 1 ? 'Finish Quiz' : 'Next Question'}
			</button>
		</div>
	</section>
{/if}
