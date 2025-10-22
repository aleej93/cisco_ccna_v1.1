<script lang="ts">
	import TopicCard, { type Topic } from '$lib/components/TopicCard.svelte';
	import { resolve } from '$app/paths';

	const topics: Topic[] = [
		{
			id: '1.1',
			title: 'Explain the role and function of network components',
			subtopics: [
				{ id: '1.1.a', label: 'Routers', href: '/study/1.1.a' },
				{ id: '1.1.b', label: 'Layer 2 and Layer 3 switches', href: '/study/1.1.b' },
				{ id: '1.1.c', label: 'Next-generation firewalls and IPS', href: '/study/1.1.c' },
				{ id: '1.1.d', label: 'Access points', href: '/study/1.1.d' },
				{ id: '1.1.e', label: 'Controllers', href: '/study/1.1.e' },
				{ id: '1.1.f', label: 'Endpoints', href: '/study/1.1.f' },
				{ id: '1.1.g', label: 'Servers', href: '/study/1.1.g' },
				{ id: '1.1.h', label: 'PoE', href: '/study/1.1.h' }
			]
		},
		{
			id: '1.2',
			title: 'Describe characteristics of network topology architectures',
			subtopics: [
				{ id: '1.2.a', label: 'Two-tier', href: '/study/1.2.a' },
				{ id: '1.2.b', label: 'Three-tier', href: '/study/1.2.b' },
				{ id: '1.2.c', label: 'Spine-leaf', href: '/study/1.2.c' },
				{ id: '1.2.d', label: 'WAN', href: '/study/1.2.d' },
				{ id: '1.2.e', label: 'Small office/home office (SOHO)', href: '/study/1.2.e' },
				{ id: '1.2.f', label: 'On-premises and cloud', href: '/study/1.2.f' }
			]
		},
		{
			id: '1.3',
			title: 'Compare physical interface and cabling types',
			subtopics: [
				{
					id: '1.3.a',
					label: 'Single-mode fiber, multimode fiber, copper',
					href: '/study/1.3.a'
				},
				{
					id: '1.3.b',
					label: 'Connections (Ethernet shared media and point-to-point)',
					href: '/study/1.3.b'
				}
			]
		},
		{
			id: '1.4',
			title:
				'Identify interface and cable issues (collisions, errors, mismatch duplex, and/or speed)',
			href: '/study/1.4'
		},
		{
			id: '1.5',
			title: 'Compare TCP to UDP',
			href: '/study/1.5'
		},
		{
			id: '1.6',
			title: 'Configure and verify IPv4 addressing and subnetting',
			href: '/study/1.6'
		},
		{
			id: '1.7',
			title: 'Describe private IPv4 addressing',
			href: '/study/1.7'
		},
		{
			id: '1.8',
			title: 'Configure and verify IPv6 addressing and prefix',
			href: '/study/1.8'
		},
		{
			id: '1.9',
			title: 'Describe IPv6 address types',
			subtopics: [
				{
					id: '1.9.a',
					label: 'Unicast (global, unique local, and link local)',
					href: '/study/1.9.a'
				},
				{ id: '1.9.b', label: 'Anycast', href: '/study/1.9.b' },
				{ id: '1.9.c', label: 'Multicast', href: '/study/1.9.c' },
				{ id: '1.9.d', label: 'Modified EUI 64', href: '/study/1.9.d' }
			]
		},
		{
			id: '1.10',
			title: 'Verify IP parameters for Client OS (Windows, Mac OS, Linux)',
			href: '/study/1.10'
		},
		{
			id: '1.11',
			title: 'Describe wireless principles',
			subtopics: [
				{ id: '1.11.a', label: 'Nonoverlapping Wi-Fi channels', href: '/study/1.11.a' },
				{ id: '1.11.b', label: 'SSID', href: '/study/1.11.b' },
				{ id: '1.11.c', label: 'RF', href: '/study/1.11.c' },
				{ id: '1.11.d', label: 'Encryption', href: '/study/1.11.d' }
			]
		},
		{
			id: '1.12',
			title: 'Explain virtualization fundamentals (server virtualization, containers, and VRFs)',
			href: '/study/1.12'
		},
		{
			id: '1.13',
			title: 'Describe switching concepts',
			subtopics: [
				{ id: '1.13.a', label: 'MAC learning and aging', href: '/study/1.13.a' },
				{ id: '1.13.b', label: 'Frame switching', href: '/study/1.13.b' },
				{ id: '1.13.c', label: 'Frame flooding', href: '/study/1.13.c' },
				{ id: '1.13.d', label: 'MAC address table', href: '/study/1.13.d' }
			]
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
			<h1 class="mb-2 text-4xl font-bold text-black">Domain 1.0 - Network Fundamentals</h1>
			<p class="text-xl text-gray-600">20% of exam</p>
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
