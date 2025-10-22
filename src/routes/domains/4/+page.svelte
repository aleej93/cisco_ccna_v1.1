<script lang="ts">
	import TopicCard, { type Topic } from '$lib/components/TopicCard.svelte';
	import { resolve } from '$app/paths';

	const topics: Topic[] = [
		{
			id: '4.1',
			title: 'Configure and verify inside source NAT using static and pools',
			href: '/study/4.1'
		},
		{
			id: '4.2',
			title: 'Configure and verify NTP operating in a client and server mode',
			href: '/study/4.2'
		},
		{
			id: '4.3',
			title: 'Explain the role of DHCP and DNS within the network',
			href: '/study/4.3'
		},
		{
			id: '4.4',
			title: 'Explain the function of SNMP in network operations',
			href: '/study/4.4'
		},
		{
			id: '4.5',
			title: 'Describe the use of syslog features, including facilities and severity levels',
			href: '/study/4.5'
		},
		{
			id: '4.6',
			title: 'Configure and verify DHCP client and relay',
			href: '/study/4.6'
		},
		{
			id: '4.7',
			title:
				'Explain the forwarding per-hop behavior (PHB) for QoS such as classification, marking, queuing, congestion, policing, and shaping',
			href: '/study/4.7'
		},
		{
			id: '4.8',
			title: 'Configure network devices for remote access using SSH',
			href: '/study/4.8'
		},
		{
			id: '4.9',
			title: 'Describe the capabilities and functions of TFTP/FTP in the network',
			href: '/study/4.9'
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
			<h1 class="mb-2 text-4xl font-bold text-black">Domain 4.0 - IP Services</h1>
			<p class="text-xl text-gray-600">10% of exam</p>
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
