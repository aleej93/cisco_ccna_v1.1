<script lang="ts">
	import TopicCard, { type Topic } from '$lib/components/TopicCard.svelte';
	import { resolve } from '$app/paths';

	const topics: Topic[] = [
		{
			id: '2.1',
			title: 'Configure and verify VLANs (normal range) spanning multiple switches',
			subtopics: [
				{ id: '2.1.a', label: 'Access ports (data and voice)', href: '/study/2.1.a' },
				{ id: '2.1.b', label: 'Default VLAN', href: '/study/2.1.b' },
				{ id: '2.1.c', label: 'InterVLAN connectivity', href: '/study/2.1.c' }
			]
		},
		{
			id: '2.2',
			title: 'Configure and verify interswitch connectivity',
			subtopics: [
				{ id: '2.2.a', label: 'Trunk ports', href: '/study/2.2.a' },
				{ id: '2.2.b', label: '802.1Q', href: '/study/2.2.b' },
				{ id: '2.2.c', label: 'Native VLAN', href: '/study/2.2.c' }
			]
		},
		{
			id: '2.3',
			title: 'Configure and verify Layer 2 discovery protocols (Cisco Discovery Protocol and LLDP)',
			href: '/study/2.3'
		},
		{
			id: '2.4',
			title: 'Configure and verify (Layer 2/Layer 3) EtherChannel (LACP)',
			href: '/study/2.4'
		},
		{
			id: '2.5',
			title: 'Interpret basic operations of Rapid PVST+ Spanning Tree Protocol',
			subtopics: [
				{
					id: '2.5.a',
					label: 'Root port, root bridge (primary/secondary), and other port names',
					href: '/study/2.5.a'
				},
				{ id: '2.5.b', label: 'Port states and roles', href: '/study/2.5.b' },
				{ id: '2.5.c', label: 'PortFast', href: '/study/2.5.c' },
				{
					id: '2.5.d',
					label: 'Root guard, loop guard, BPDU filter, and BPDU guard',
					href: '/study/2.5.d'
				}
			]
		},
		{
			id: '2.6',
			title: 'Describe Cisco Wireless Architectures and AP modes',
			href: '/study/2.6'
		},
		{
			id: '2.7',
			title:
				'Describe physical infrastructure connections of WLAN components (AP, WLC, access/trunk ports, and LAG)',
			href: '/study/2.7'
		},
		{
			id: '2.8',
			title:
				'Describe network device management access (Telnet, SSH, HTTP, HTTPS, console, TACACS+/RADIUS, and cloud managed)',
			href: '/study/2.8'
		},
		{
			id: '2.9',
			title:
				'Interpret the wireless LAN GUI configuration for client connectivity, such as WLAN creation, security settings, QoS profiles, and advanced settings',
			href: '/study/2.9'
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
			<h1 class="mb-2 text-4xl font-bold text-black">Domain 2.0 - Network Access</h1>
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
