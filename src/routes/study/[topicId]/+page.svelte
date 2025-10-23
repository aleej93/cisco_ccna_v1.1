<script lang="ts">
	/**
	 * Study Page Template
	 * Dynamic route for individual topic/subtopic study pages
	 */

	import { page } from '$app/stores';
	import { resolve } from '$app/paths';
	import PracticeQuiz from '$lib/components/PracticeQuiz.svelte';
	import quizRouters from '$lib/content/domain-1/1.1a-routers/practice-quiz.json';
	import type { ComponentType } from 'svelte';

	// TypeScript interface for tab structure
	interface Tab {
		id: string;
		label: string;
		icon: string;
	}

	// Get the topic ID from URL parameters with fallback
	$: topicId = $page.params.topicId || '';

	// Reactive state for active tab
	let activeTab = 'study';

	// Store for the loaded markdown component
	let MarkdownContent: ComponentType | null = null;
	let contentLoading = true;

	// Use Vite's glob import to eagerly load all markdown files
	const allMarkdownModules = import.meta.glob<{ default: ComponentType }>(
		'../../../lib/content/**/*.md',
		{ eager: true }
	);

	// Map topic IDs to file paths
	const topicPaths: { [key: string]: string } = {
		'1.1.a': '../../../lib/content/domain-1/1.1a-routers/study-material.md'
		// Add more mappings as you create content
	};

	// Load markdown content when topicId changes
	$: {
		if (topicId) {
			loadMarkdownContent(topicId);
		}
	}

	function loadMarkdownContent(id: string) {
		contentLoading = true;
		MarkdownContent = null;

		const filePath = topicPaths[id];
		if (!filePath) {
			contentLoading = false;
			return;
		}

		try {
			// Get the module from the pre-loaded glob
			const module = allMarkdownModules[filePath];

			if (module?.default) {
				MarkdownContent = module.default;
			} else {
				console.error(`Markdown module not found for path: ${filePath}`);
				console.log('Available modules:', Object.keys(allMarkdownModules));
			}
		} catch (err) {
			console.error(`Failed to load markdown for ${id}:`, err);
		} finally {
			contentLoading = false;
		}
	}

	// Tab definitions
	const tabs: Tab[] = [
		{ id: 'study', label: 'Study Material', icon: '📖' },
		{ id: 'quiz', label: 'Practice Quiz', icon: '✅' },
		{ id: 'real-world', label: 'Real World', icon: '💡' },
		{ id: 'exam-tips', label: 'Exam Tips', icon: '🎓' },
		{ id: 'resources', label: 'Resources', icon: '🔗' },
		{ id: 'commands', label: 'Commands', icon: '⌨️' }
	];

	// Function to switch tabs
	function setActiveTab(tabId: string) {
		activeTab = tabId;
	}

	// Placeholder: Extract domain number from topicId (e.g., "1.1.a" -> "1.0")
	function getDomainNumber(id: string): string {
		const parts = id.split('.');
		return parts[0] + '.0';
	}

	// Placeholder: Get domain name (in real app, this would come from data)
	function getDomainName(id: string): string {
		const domainMap: { [key: string]: string } = {
			'1.0': 'Network Fundamentals',
			'2.0': 'Network Access',
			'3.0': 'IP Connectivity',
			'4.0': 'IP Services',
			'5.0': 'Security Fundamentals',
			'6.0': 'Automation and Programmability'
		};
		return domainMap[getDomainNumber(id)] || 'Unknown Domain';
	}

	// Topic name mapping (comprehensive list of all topics and subtopics)
	const topicNames: { [key: string]: string } = {
		// Domain 1.0 - Network Fundamentals
		'1.1': 'Role and Function of Network Components',
		'1.1.a': 'Routers',
		'1.1.b': 'Layer 2 and Layer 3 Switches',
		'1.1.c': 'Next-Generation Firewalls and IPS',
		'1.1.d': 'Access Points',
		'1.1.e': 'Controllers',
		'1.1.f': 'Endpoints',
		'1.1.g': 'Servers',
		'1.1.h': 'PoE',
		'1.2': 'Network Topology Architectures',
		'1.2.a': 'Two-Tier',
		'1.2.b': 'Three-Tier',
		'1.2.c': 'Spine-Leaf',
		'1.2.d': 'WAN',
		'1.2.e': 'Small Office/Home Office (SOHO)',
		'1.2.f': 'On-Premises and Cloud',
		'1.3': 'Physical Interface and Cabling Types',
		'1.3.a': 'Single-Mode Fiber, Multimode Fiber, Copper',
		'1.3.b': 'Connections (Ethernet Shared Media and Point-to-Point)',
		'1.4': 'Interface and Cable Issues',
		'1.5': 'TCP vs UDP',
		'1.6': 'IPv4 Addressing and Subnetting',
		'1.7': 'Private IPv4 Addressing',
		'1.8': 'IPv6 Addressing and Prefix',
		'1.9': 'IPv6 Address Types',
		'1.9.a': 'Unicast (Global, Unique Local, and Link Local)',
		'1.9.b': 'Anycast',
		'1.9.c': 'Multicast',
		'1.9.d': 'Modified EUI 64',
		'1.10': 'IP Parameters for Client OS',
		'1.11': 'Wireless Principles',
		'1.11.a': 'Nonoverlapping Wi-Fi Channels',
		'1.11.b': 'SSID',
		'1.11.c': 'RF',
		'1.11.d': 'Encryption',
		'1.12': 'Virtualization Fundamentals',
		'1.13': 'Switching Concepts',
		'1.13.a': 'MAC Learning and Aging',
		'1.13.b': 'Frame Switching',
		'1.13.c': 'Frame Flooding',
		'1.13.d': 'MAC Address Table',

		// Domain 2.0 - Network Access
		'2.1': 'VLANs (Normal Range) Spanning Multiple Switches',
		'2.1.a': 'Access Ports (Data and Voice)',
		'2.1.b': 'Default VLAN',
		'2.1.c': 'InterVLAN Connectivity',
		'2.2': 'Interswitch Connectivity',
		'2.2.a': 'Trunk Ports',
		'2.2.b': '802.1Q',
		'2.2.c': 'Native VLAN',
		'2.3': 'Layer 2 Discovery Protocols (CDP and LLDP)',
		'2.4': 'EtherChannel (LACP)',
		'2.5': 'Rapid PVST+ Spanning Tree Protocol',
		'2.5.a': 'Root Port, Root Bridge, and Other Port Names',
		'2.5.b': 'Port States and Roles',
		'2.5.c': 'PortFast',
		'2.5.d': 'Root Guard, Loop Guard, BPDU Filter, and BPDU Guard',
		'2.6': 'Cisco Wireless Architectures and AP Modes',
		'2.7': 'Physical Infrastructure Connections of WLAN Components',
		'2.8': 'Network Device Management Access',
		'2.9': 'Wireless LAN GUI Configuration',

		// Domain 3.0 - IP Connectivity
		'3.1': 'Components of Routing Table',
		'3.1.a': 'Routing Protocol Code',
		'3.1.b': 'Prefix',
		'3.1.c': 'Network Mask',
		'3.1.d': 'Next Hop',
		'3.1.e': 'Administrative Distance',
		'3.1.f': 'Metric',
		'3.1.g': 'Gateway of Last Resort',
		'3.2': 'Router Forwarding Decision',
		'3.2.a': 'Longest Prefix Match',
		'3.2.b': 'Administrative Distance',
		'3.2.c': 'Routing Protocol Metric',
		'3.3': 'IPv4 and IPv6 Static Routing',
		'3.3.a': 'Default Route',
		'3.3.b': 'Network Route',
		'3.3.c': 'Host Route',
		'3.3.d': 'Floating Static',
		'3.4': 'Single Area OSPFv2',
		'3.4.a': 'Neighbor Adjacencies',
		'3.4.b': 'Point-to-Point',
		'3.4.c': 'Broadcast (DR/BDR Selection)',
		'3.4.d': 'Router ID',
		'3.5': 'First Hop Redundancy Protocols',

		// Domain 4.0 - IP Services
		'4.1': 'Inside Source NAT Using Static and Pools',
		'4.2': 'NTP Operating in Client and Server Mode',
		'4.3': 'Role of DHCP and DNS',
		'4.4': 'Function of SNMP',
		'4.5': 'Syslog Features',
		'4.6': 'DHCP Client and Relay',
		'4.7': 'QoS Forwarding Per-Hop Behavior (PHB)',
		'4.8': 'Remote Access Using SSH',
		'4.9': 'TFTP/FTP in the Network',

		// Domain 5.0 - Security Fundamentals
		'5.1': 'Key Security Concepts',
		'5.2': 'Security Program Elements',
		'5.3': 'Device Access Control Using Local Passwords',
		'5.4': 'Security Password Policy Elements',
		'5.5': 'IPsec Remote Access and Site-to-Site VPNs',
		'5.6': 'Access Control Lists',
		'5.7': 'Layer 2 Security Features',
		'5.8': 'Authentication, Authorization, and Accounting',
		'5.9': 'Wireless Security Protocols',
		'5.10': 'WLAN Configuration Using WPA2 PSK',

		// Domain 6.0 - Automation and Programmability
		'6.1': 'How Automation Impacts Network Management',
		'6.2': 'Traditional vs Controller-Based Networking',
		'6.3': 'Controller-Based Software Defined Architecture',
		'6.4': 'AI and Machine Learning in Network Operations',
		'6.5': 'Characteristics of REST-Based APIs',
		'6.6': 'Configuration Management Mechanisms',
		'6.7': 'Components of JSON-Encoded Data'
	};

	// Get topic title from mapping or fallback to generic title
	function getTopicTitle(id: string): string {
		return topicNames[id] || `Topic ${id}`;
	}

	// Topic order for each domain (for navigation)
	const domainTopicOrder: { [key: string]: string[] } = {
		'1': [
			'1.1.a',
			'1.1.b',
			'1.1.c',
			'1.1.d',
			'1.1.e',
			'1.1.f',
			'1.1.g',
			'1.1.h',
			'1.2.a',
			'1.2.b',
			'1.2.c',
			'1.2.d',
			'1.2.e',
			'1.2.f',
			'1.3.a',
			'1.3.b',
			'1.4',
			'1.5',
			'1.6',
			'1.7',
			'1.8',
			'1.9.a',
			'1.9.b',
			'1.9.c',
			'1.9.d',
			'1.10',
			'1.11.a',
			'1.11.b',
			'1.11.c',
			'1.11.d',
			'1.12',
			'1.13.a',
			'1.13.b',
			'1.13.c',
			'1.13.d'
		],
		'2': [
			'2.1.a',
			'2.1.b',
			'2.1.c',
			'2.2.a',
			'2.2.b',
			'2.2.c',
			'2.3',
			'2.4',
			'2.5.a',
			'2.5.b',
			'2.5.c',
			'2.5.d',
			'2.6',
			'2.7',
			'2.8',
			'2.9'
		],
		'3': [
			'3.1.a',
			'3.1.b',
			'3.1.c',
			'3.1.d',
			'3.1.e',
			'3.1.f',
			'3.1.g',
			'3.2.a',
			'3.2.b',
			'3.2.c',
			'3.3.a',
			'3.3.b',
			'3.3.c',
			'3.3.d',
			'3.4.a',
			'3.4.b',
			'3.4.c',
			'3.4.d',
			'3.5'
		],
		'4': ['4.1', '4.2', '4.3', '4.4', '4.5', '4.6', '4.7', '4.8', '4.9'],
		'5': ['5.1', '5.2', '5.3', '5.4', '5.5', '5.6', '5.7', '5.8', '5.9', '5.10'],
		'6': ['6.1', '6.2', '6.3', '6.4', '6.5', '6.6', '6.7']
	};

	// Get the domain number from topic ID (e.g., "1.1.a" -> "1")
	function getDomainFromTopic(id: string): string {
		return id.split('.')[0];
	}

	// Get previous topic ID
	function getPreviousTopic(id: string): string | null {
		const domain = getDomainFromTopic(id);
		const topics = domainTopicOrder[domain];
		if (!topics) return null;

		const currentIndex = topics.indexOf(id);
		if (currentIndex <= 0) return null;

		return topics[currentIndex - 1];
	}

	// Get next topic ID
	function getNextTopic(id: string): string | null {
		const domain = getDomainFromTopic(id);
		const topics = domainTopicOrder[domain];
		if (!topics) return null;

		const currentIndex = topics.indexOf(id);
		if (currentIndex === -1 || currentIndex >= topics.length - 1) return null;

		return topics[currentIndex + 1];
	}

	// Check if current topic is first in domain
	function isFirstTopic(id: string): boolean {
		const domain = getDomainFromTopic(id);
		const topics = domainTopicOrder[domain];
		if (!topics) return false;
		return topics.indexOf(id) === 0;
	}

	// Check if current topic is last in domain
	function isLastTopic(id: string): boolean {
		const domain = getDomainFromTopic(id);
		const topics = domainTopicOrder[domain];
		if (!topics) return false;
		return topics.indexOf(id) === topics.length - 1;
	}

	// Check if topic exists in navigation
	function topicExists(id: string): boolean {
		const domain = getDomainFromTopic(id);
		const topics = domainTopicOrder[domain];
		if (!topics) return false;
		return topics.includes(id);
	}

	// Reactive navigation state
	$: previousTopic = getPreviousTopic(topicId);
	$: nextTopic = getNextTopic(topicId);
	$: isFirst = isFirstTopic(topicId);
	$: isLast = isLastTopic(topicId);
	$: showNavigation = topicExists(topicId);
	$: currentDomain = getDomainFromTopic(topicId);
</script>

<div class="min-h-screen bg-white">
	<!-- Breadcrumb Navigation -->
	<nav class="w-full border-b border-gray-200 bg-gray-50 px-6 py-3">
		<div class="mx-auto max-w-7xl">
			<div class="flex items-center text-sm text-gray-600">
				<a href={resolve('/domains')} class="transition-colors hover:text-black"> CCNA 200-301 </a>
				<span class="mx-2">›</span>
				<a
					href={resolve(`/domains/${getDomainNumber(topicId).split('.')[0]}`)}
					class="transition-colors hover:text-black"
				>
					{getDomainNumber(topicId)}
					{getDomainName(topicId)}
				</a>
				<span class="mx-2">›</span>
				<span class="font-medium text-black">{topicId} {getTopicTitle(topicId)}</span>
			</div>
		</div>
	</nav>

	<!-- Main Content -->
	<main class="mx-auto max-w-7xl px-6 py-8">
		<!-- Page Title -->
		<div class="mb-8">
			<h1 class="mb-4 text-4xl font-bold text-black">
				{getTopicTitle(topicId)}
			</h1>

			<!-- Progress Bar Placeholder -->
			<div class="mb-4">
				<div class="mb-2 flex items-center justify-between">
					<span class="text-sm font-medium text-gray-600">Overall Progress</span>
					<span class="text-sm font-medium text-gray-600">20%</span>
				</div>
				<div class="h-2 w-full rounded-full bg-gray-200">
					<div class="h-2 rounded-full bg-blue-600" style="width: 20%"></div>
				</div>
			</div>
		</div>

		<!-- Tabbed Interface -->
		<div class="mb-8">
			<!-- Tab Headers -->
			<div class="mb-6 border-b border-gray-200">
				<div class="flex flex-wrap gap-2">
					{#each tabs as tab (tab.id)}
						<button
							on:click={() => setActiveTab(tab.id)}
							class="px-4 py-3 text-sm font-medium transition-all duration-200
                     {activeTab === tab.id
								? 'border-b-2 border-blue-600 text-blue-600'
								: 'text-gray-600 hover:text-black'}"
						>
							<span class="mr-2">{tab.icon}</span>
							{tab.label}
						</button>
					{/each}
				</div>
			</div>

			<!-- Tab Content Area -->
			<div class="min-h-[400px] rounded-lg border border-gray-200 bg-white p-8">
				{#if activeTab === 'study'}
					{#if contentLoading}
						<div class="text-gray-600">
							<p>Loading study material...</p>
						</div>
					{:else if MarkdownContent}
						<!-- Render Markdown Content with Tailwind Typography -->
						<div class="space-y-10">
							<article
								class="prose prose-lg max-w-none
	                           prose-headings:font-bold prose-headings:text-black
	                           prose-h1:text-3xl prose-h2:text-2xl prose-h3:text-xl
                           prose-p:leading-relaxed prose-p:text-gray-700
                           prose-a:text-blue-600 prose-a:no-underline hover:prose-a:underline
                           prose-blockquote:border-l-4 prose-blockquote:border-blue-500
                           prose-blockquote:pl-4 prose-blockquote:italic prose-strong:font-semibold prose-strong:text-black prose-code:rounded prose-code:bg-gray-100
                           prose-code:px-2 prose-code:py-1
                           prose-code:text-sm prose-code:text-gray-800
                           prose-pre:bg-gray-900 prose-pre:text-gray-100 prose-ol:list-decimal prose-ol:pl-6 prose-ul:list-disc
                           prose-ul:pl-6 prose-li:text-gray-700 prose-table:w-full prose-table:border-collapse
                           prose-th:border prose-th:border-gray-300
                           prose-th:bg-gray-100 prose-th:px-4
                           prose-th:py-2
                           prose-td:border prose-td:border-gray-300 prose-td:px-4 prose-td:py-2"
							>
								<svelte:component this={MarkdownContent} />
							</article>
						</div>
					{:else}
						<div class="text-gray-600">
							<h2 class="mb-4 text-2xl font-bold text-black">Study Material</h2>
							<p>Study content for this topic is coming soon...</p>
						</div>
					{/if}
				{:else if activeTab === 'quiz'}
					{#if topicId === '1.1.a'}
						<PracticeQuiz questions={quizRouters} />
					{:else}
						<div class="text-gray-600">
							<h2 class="mb-4 text-2xl font-bold text-black">Practice Quiz</h2>
							<p>Quiz questions will go here.</p>
						</div>
					{/if}
				{:else if activeTab === 'real-world'}
					<div class="text-gray-600">
						<h2 class="mb-4 text-2xl font-bold text-black">Real World Examples</h2>
						<p>Real-world examples will go here</p>
					</div>
				{:else if activeTab === 'exam-tips'}
					<div class="text-gray-600">
						<h2 class="mb-4 text-2xl font-bold text-black">Exam Tips</h2>
						<p>Exam tips will go here</p>
					</div>
				{:else if activeTab === 'resources'}
					<div class="text-gray-600">
						<h2 class="mb-4 text-2xl font-bold text-black">Resources</h2>
						<p>Links and resources will go here</p>
					</div>
				{:else if activeTab === 'commands'}
					<div class="text-gray-600">
						<h2 class="mb-4 text-2xl font-bold text-black">CLI Commands</h2>
						<p>CLI commands will go here</p>
					</div>
				{/if}
			</div>
		</div>

		<!-- Navigation Buttons (Prev/Next Topic) -->
		{#if showNavigation}
			<div class="mt-8 flex items-center justify-between border-t border-gray-200 pt-6">
				<!-- Previous Button -->
				{#if isFirst}
					<!-- First topic: Back to Domain -->
					<a
						href={resolve(`/domains/${currentDomain}`)}
						class="rounded-lg border-2 border-black bg-white px-6 py-3 font-medium text-black
	                   transition-all duration-200 hover:bg-gray-50"
					>
						← Back to Domain {currentDomain}.0
					</a>
				{:else if previousTopic}
					<!-- Middle topics: Previous Topic -->
					<a
						href={resolve(`/study/${previousTopic}`)}
						class="rounded-lg border-2 border-black bg-white px-6 py-3 font-medium text-black
	                   transition-all duration-200 hover:bg-gray-50"
					>
						← Previous Topic
					</a>
				{/if}

				<!-- Next Button -->
				{#if isLast}
					<!-- Last topic: Domain Complete -->
					<a
						href={resolve('/domains')}
						class="flex items-center rounded-lg bg-black px-6 py-3
	                   font-medium text-white transition-all duration-200 hover:bg-gray-800"
					>
						<span class="mr-2">✓</span>
						Domain {currentDomain}.0 Complete! Return to Domains
					</a>
				{:else if nextTopic}
					<!-- Middle topics: Next Topic -->
					<a
						href={resolve(`/study/${nextTopic}`)}
						class="rounded-lg bg-black px-6 py-3 font-medium text-white
	                   transition-all duration-200 hover:bg-gray-800"
					>
						Next Topic →
					</a>
				{/if}
			</div>
		{/if}
	</main>
</div>

<style>
	/* Ensure smooth tab transitions */
	button {
		cursor: pointer;
	}
</style>
