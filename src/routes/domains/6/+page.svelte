<script lang="ts">
	import TopicCard, { type Topic } from '$lib/components/TopicCard.svelte';
	import { resolve } from '$app/paths';

	const topics: Topic[] = [
		{
			id: '6.1',
			title: 'Explain how automation impacts network management',
			href: '/study/6.1'
		},
		{
			id: '6.2',
			title: 'Compare traditional networks with controller-based networking',
			href: '/study/6.2'
		},
		{
			id: '6.3',
			title:
				'Describe controller-based, software defined architecture (overlay, underlay, and fabric; separation of control plane and data plane; northbound and southbound APIs)',
			href: '/study/6.3'
		},
		{
			id: '6.4',
			title: 'Explain AI (generative and predictive) and machine learning in network operations',
			href: '/study/6.4'
		},
		{
			id: '6.5',
			title:
				'Describe characteristics of REST-based APIs (authentication types, CRUD, HTTP verbs, and data encoding)',
			href: '/study/6.5'
		},
		{
			id: '6.6',
			title:
				'Recognize the capabilities of configuration management mechanisms such as Ansible and Terraform',
			href: '/study/6.6'
		},
		{
			id: '6.7',
			title: 'Recognize components of JSON-encoded data',
			href: '/study/6.7'
		}
	];

	const domainsHref = resolve('/domains');
</script>

<div class="min-h-screen bg-white">
	<nav class="w-full border-b border-gray-200 px-6 py-4">
		<div class="mx-auto max-w-7xl">
			<a
				href={domainsHref}
				class="inline-flex items-center text-black transition-colors duration-200 hover:text-gray-600"
			>
				<span class="text-lg">←</span>
				<span class="ml-2 font-medium">Back to Domains</span>
			</a>
		</div>
	</nav>

	<main class="flex flex-col items-center justify-center px-6 py-16">
		<div class="mb-12 text-center">
			<h1 class="mb-2 text-4xl font-bold text-black">
				Domain 6.0 - Automation and Programmability
			</h1>
			<p class="text-xl text-gray-600">10% of exam</p>
		</div>

		<div class="mb-6 w-full max-w-[600px]">
			<h2 class="text-2xl font-bold text-black">Topics</h2>
		</div>

		<div class="flex w-full flex-col items-center gap-4">
			{#each topics as topic (topic.id)}
				<TopicCard {topic} />
			{/each}
		</div>
	</main>
</div>
