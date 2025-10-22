<script lang="ts">
	import { resolve } from '$app/paths';

	export interface Subtopic {
		id: string;
		label: string;
		href: string;
	}

	export interface Topic {
		id: string;
		title: string;
		href?: string;
		subtopics?: Subtopic[];
	}

	export let topic: Topic;

	let hasSubtopics = false;
	let open = false;

	$: hasSubtopics = Array.isArray(topic.subtopics) && topic.subtopics.length > 0;

	const sanitizedId = topic.id.replace(/[^a-zA-Z0-9_-]/g, '-');
	const toggleId = `toggle-${sanitizedId}`;
	const panelId = `panel-${sanitizedId}`;

	const baseClasses =
		'topic-card w-[600px] px-6 py-4 bg-black rounded-xl transition-all duration-200 ease-in-out hover:scale-105 hover:shadow-lg focus:outline-none focus-visible:ring-2 focus-visible:ring-gray-400 focus-visible:ring-offset-2 text-left';

	function onToggle() {
		if (!hasSubtopics) return;
		open = !open;
	}
</script>

{#if hasSubtopics}
	<div class="flex w-full flex-col items-center">
		<button
			type="button"
			id={toggleId}
			aria-expanded={open}
			aria-controls={panelId}
			class={`${baseClasses} cursor-pointer`}
			on:click={onToggle}
		>
			<div class="flex items-start justify-between">
				<div class="flex-1">
					<div class="mb-1 text-sm font-bold text-white opacity-80">{topic.id}</div>
					<div class="text-base font-medium text-white">{topic.title}</div>
				</div>
				<svg
					class="ml-4 h-5 w-5 flex-shrink-0 transform text-white transition-transform duration-200"
					class:rotate-180={open}
					viewBox="0 0 20 20"
					fill="currentColor"
					aria-hidden="true"
				>
					<path
						fill-rule="evenodd"
						d="M5.23 7.21a.75.75 0 011.06.02L10 11.175l3.71-3.944a.75.75 0 111.08 1.04l-4.25 4.515a.75.75 0 01-1.08 0L5.21 8.27a.75.75 0 01.02-1.06z"
						clip-rule="evenodd"
					/>
				</svg>
			</div>
		</button>

		{#if open}
			<div
				id={panelId}
				role="region"
				aria-labelledby={toggleId}
				class="mt-3 flex w-full flex-col items-center gap-3"
			>
				{#each topic.subtopics ?? [] as subtopic (subtopic.id)}
					<a
						href={resolve(subtopic.href)}
						class="subtopic-card ml-12 w-[550px] rounded-lg bg-gray-800 px-5 py-3 text-left no-underline transition-all duration-200 ease-in-out hover:scale-105 hover:shadow-lg focus:outline-none focus-visible:ring-2 focus-visible:ring-gray-400 focus-visible:ring-offset-2"
					>
						<div class="mb-1 text-xs font-bold text-white opacity-70">{subtopic.id}</div>
						<div class="text-sm font-medium text-white">{subtopic.label}</div>
					</a>
				{/each}
			</div>
		{/if}
	</div>
{:else if topic.href}
	<a href={resolve(topic.href)} class={`${baseClasses} flex flex-col items-start no-underline`}>
		<div class="mb-1 text-sm font-bold text-white opacity-80">{topic.id}</div>
		<div class="text-base font-medium text-white">{topic.title}</div>
	</a>
{:else}
	<div class={`${baseClasses} flex flex-col items-start`}>
		<div class="mb-1 text-sm font-bold text-white opacity-80">{topic.id}</div>
		<div class="text-base font-medium text-white">{topic.title}</div>
	</div>
{/if}
