<script lang="ts">
	import TopicCard, { type Topic } from '$lib/components/TopicCard.svelte';
	import { resolve } from '$app/paths';

	const topics: Topic[] = [
		{
			id: '3.1',
			title: 'Interpret the components of routing table',
			subtopics: [
				{ id: '3.1.a', label: 'Routing protocol code', href: '/study/3.1.a' },
				{ id: '3.1.b', label: 'Prefix', href: '/study/3.1.b' },
				{ id: '3.1.c', label: 'Network mask', href: '/study/3.1.c' },
				{ id: '3.1.d', label: 'Next hop', href: '/study/3.1.d' },
				{ id: '3.1.e', label: 'Administrative distance', href: '/study/3.1.e' },
				{ id: '3.1.f', label: 'Metric', href: '/study/3.1.f' },
				{ id: '3.1.g', label: 'Gateway of last resort', href: '/study/3.1.g' }
			]
		},
		{
			id: '3.2',
			title: 'Determine how a router makes a forwarding decision by default',
			subtopics: [
				{ id: '3.2.a', label: 'Longest prefix match', href: '/study/3.2.a' },
				{ id: '3.2.b', label: 'Administrative distance', href: '/study/3.2.b' },
				{ id: '3.2.c', label: 'Routing protocol metric', href: '/study/3.2.c' }
			]
		},
		{
			id: '3.3',
			title: 'Configure and verify IPv4 and IPv6 static routing',
			subtopics: [
				{ id: '3.3.a', label: 'Default route', href: '/study/3.3.a' },
				{ id: '3.3.b', label: 'Network route', href: '/study/3.3.b' },
				{ id: '3.3.c', label: 'Host route', href: '/study/3.3.c' },
				{ id: '3.3.d', label: 'Floating static', href: '/study/3.3.d' }
			]
		},
		{
			id: '3.4',
			title: 'Configure and verify single area OSPFv2',
			subtopics: [
				{ id: '3.4.a', label: 'Neighbor adjacencies', href: '/study/3.4.a' },
				{ id: '3.4.b', label: 'Point-to-point', href: '/study/3.4.b' },
				{ id: '3.4.c', label: 'Broadcast (DR/BDR selection)', href: '/study/3.4.c' },
				{ id: '3.4.d', label: 'Router ID', href: '/study/3.4.d' }
			]
		},
		{
			id: '3.5',
			title: 'Describe the purpose, functions, and concepts of first hop redundancy protocols',
			href: '/study/3.5'
		}
	];

	const domainsHref = resolve('/domains');
</script>

<div class="min-h-screen bg-white">
	<!-- Navigation Bar with Back Button -->
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

	<!-- Main Content -->
	<main class="flex flex-col items-center justify-center px-6 py-16">
		<!-- Page Title and Subtitle -->
		<div class="mb-12 text-center">
			<h1 class="mb-2 text-4xl font-bold text-black">Domain 3.0 - IP Connectivity</h1>
			<p class="text-xl text-gray-600">25% of exam</p>
		</div>

		<!-- Section Header -->
		<div class="mb-6 w-full max-w-[600px]">
			<h2 class="text-2xl font-bold text-black">Topics</h2>
		</div>

		<!-- Topic Cards - Centered Vertical Stack -->
		<div class="flex w-full flex-col items-center gap-4">
			{#each topics as topic (topic.id)}
				<TopicCard {topic} />
			{/each}
		</div>
	</main>
</div>
