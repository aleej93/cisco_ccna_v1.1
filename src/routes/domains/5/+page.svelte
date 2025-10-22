<script lang="ts">
	import TopicCard, { type Topic } from '$lib/components/TopicCard.svelte';
	import { resolve } from '$app/paths';

	const topics: Topic[] = [
		{
			id: '5.1',
			title:
				'Define key security concepts (threats, vulnerabilities, exploits, and mitigation techniques)',
			href: '/study/5.1'
		},
		{
			id: '5.2',
			title:
				'Describe security program elements (user awareness, training, and physical access control)',
			href: '/study/5.2'
		},
		{
			id: '5.3',
			title: 'Configure and verify device access control using local passwords',
			href: '/study/5.3'
		},
		{
			id: '5.4',
			title:
				'Describe security password policy elements, such as management, complexity, and password alternatives (multifactor authentication, certificates, and biometrics)',
			href: '/study/5.4'
		},
		{
			id: '5.5',
			title: 'Describe IPsec remote access and site-to-site VPNs',
			href: '/study/5.5'
		},
		{
			id: '5.6',
			title: 'Configure and verify access control lists',
			href: '/study/5.6'
		},
		{
			id: '5.7',
			title:
				'Configure and verify Layer 2 security features (DHCP snooping, dynamic ARP inspection, and port security)',
			href: '/study/5.7'
		},
		{
			id: '5.8',
			title: 'Compare authentication, authorization, and accounting concepts',
			href: '/study/5.8'
		},
		{
			id: '5.9',
			title: 'Describe wireless security protocols (WPA, WPA2, and WPA3)',
			href: '/study/5.9'
		},
		{
			id: '5.10',
			title: 'Configure and verify WLAN within the GUI using WPA2 PSK',
			href: '/study/5.10'
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
			<h1 class="mb-2 text-4xl font-bold text-black">Domain 5.0 - Security Fundamentals</h1>
			<p class="text-xl text-gray-600">15% of exam</p>
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
