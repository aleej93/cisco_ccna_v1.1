<script lang="ts">
  /**
   * Domain 1.0 - Network Fundamentals Detail Page
   * Lists all topics and subtopics within this domain
   */

  // TypeScript interfaces for hierarchical structure
  interface Subtopic {
    id: string;
    title: string;
  }

  interface Topic {
    id: string;
    title: string;
    subtopics?: Subtopic[];
  }

  // Reactive state for tracking expanded topics
  let expandedTopics: Set<string> = new Set();

  // Toggle expand/collapse for a topic
  function toggleTopic(topicId: string) {
    if (expandedTopics.has(topicId)) {
      expandedTopics.delete(topicId);
    } else {
      expandedTopics.add(topicId);
    }
    expandedTopics = expandedTopics; // Trigger reactivity
  }

  // Domain 1.0 Topics with Subtopics (from official CCNA 200-301 v1.1 blueprint)
  const topics: Topic[] = [
    {
      id: '1.1',
      title: 'Explain the role and function of network components',
      subtopics: [
        { id: '1.1.a', title: 'Routers' },
        { id: '1.1.b', title: 'Layer 2 and Layer 3 switches' },
        { id: '1.1.c', title: 'Next-generation firewalls and IPS' },
        { id: '1.1.d', title: 'Access points' },
        { id: '1.1.e', title: 'Controllers' },
        { id: '1.1.f', title: 'Endpoints' },
        { id: '1.1.g', title: 'Servers' },
        { id: '1.1.h', title: 'PoE' }
      ]
    },
    {
      id: '1.2',
      title: 'Describe characteristics of network topology architectures',
      subtopics: [
        { id: '1.2.a', title: 'Two-tier' },
        { id: '1.2.b', title: 'Three-tier' },
        { id: '1.2.c', title: 'Spine-leaf' },
        { id: '1.2.d', title: 'WAN' },
        { id: '1.2.e', title: 'Small office/home office (SOHO)' },
        { id: '1.2.f', title: 'On-premises and cloud' }
      ]
    },
    {
      id: '1.3',
      title: 'Compare physical interface and cabling types',
      subtopics: [
        { id: '1.3.a', title: 'Single-mode fiber, multimode fiber, copper' },
        { id: '1.3.b', title: 'Connections (Ethernet shared media and point-to-point)' }
      ]
    },
    {
      id: '1.4',
      title: 'Identify interface and cable issues (collisions, errors, mismatch duplex, and/or speed)'
    },
    {
      id: '1.5',
      title: 'Compare TCP to UDP'
    },
    {
      id: '1.6',
      title: 'Configure and verify IPv4 addressing and subnetting'
    },
    {
      id: '1.7',
      title: 'Describe private IPv4 addressing'
    },
    {
      id: '1.8',
      title: 'Configure and verify IPv6 addressing and prefix'
    },
    {
      id: '1.9',
      title: 'Describe IPv6 address types',
      subtopics: [
        { id: '1.9.a', title: 'Unicast (global, unique local, and link local)' },
        { id: '1.9.b', title: 'Anycast' },
        { id: '1.9.c', title: 'Multicast' },
        { id: '1.9.d', title: 'Modified EUI 64' }
      ]
    },
    {
      id: '1.10',
      title: 'Verify IP parameters for Client OS (Windows, Mac OS, Linux)'
    },
    {
      id: '1.11',
      title: 'Describe wireless principles',
      subtopics: [
        { id: '1.11.a', title: 'Nonoverlapping Wi-Fi channels' },
        { id: '1.11.b', title: 'SSID' },
        { id: '1.11.c', title: 'RF' },
        { id: '1.11.d', title: 'Encryption' }
      ]
    },
    {
      id: '1.12',
      title: 'Explain virtualization fundamentals (server virtualization, containers, and VRFs)'
    },
    {
      id: '1.13',
      title: 'Describe switching concepts',
      subtopics: [
        { id: '1.13.a', title: 'MAC learning and aging' },
        { id: '1.13.b', title: 'Frame switching' },
        { id: '1.13.c', title: 'Frame flooding' },
        { id: '1.13.d', title: 'MAC address table' }
      ]
    }
  ];
</script>

<div class="min-h-screen bg-white">
  <!-- Navigation Bar with Back Button -->
  <nav class="w-full border-b border-gray-200 px-6 py-4">
    <div class="max-w-7xl mx-auto">
      <a
        href="/domains"
        class="inline-flex items-center text-black hover:text-gray-600 transition-colors duration-200"
      >
        <span class="text-lg">←</span>
        <span class="ml-2 font-medium">Back to Domains</span>
      </a>
    </div>
  </nav>

  <!-- Main Content -->
  <main class="flex flex-col items-center justify-center px-6 py-16">
    <!-- Page Title and Subtitle -->
    <div class="text-center mb-12">
      <h1 class="text-4xl font-bold text-black mb-2">Domain 1.0 - Network Fundamentals</h1>
      <p class="text-xl text-gray-600">20% of exam</p>
    </div>

    <!-- Section Header -->
    <div class="w-full max-w-[600px] mb-6">
      <h2 class="text-2xl font-bold text-black">Topics</h2>
    </div>

    <!-- Topic Cards - Centered Vertical Stack -->
    <div class="flex flex-col items-center gap-4 w-full">
      {#each topics as topic}
        <div class="flex flex-col items-center w-full">
          <!-- Main Topic Card -->
          {#if topic.subtopics && topic.subtopics.length > 0}
            <!-- Topic WITH subtopics - Expandable -->
            <button
              on:click={() => toggleTopic(topic.id)}
              class="topic-card w-[600px] px-6 py-4 bg-black rounded-xl
                     transition-all duration-200 ease-in-out
                     hover:scale-105 hover:shadow-lg
                     focus:outline-none focus:ring-2 focus:ring-gray-400 focus:ring-offset-2
                     text-left cursor-pointer"
            >
              <div class="flex items-start justify-between">
                <div class="flex-1">
                  <!-- Topic ID -->
                  <div class="text-sm font-bold text-white opacity-80 mb-1">
                    {topic.id}
                  </div>

                  <!-- Topic Title -->
                  <div class="text-base font-medium text-white">
                    {topic.title}
                  </div>
                </div>

                <!-- Expand/Collapse Indicator -->
                <div class="text-white text-xl ml-4 flex-shrink-0">
                  {expandedTopics.has(topic.id) ? '▲' : '▼'}
                </div>
              </div>
            </button>

            <!-- Subtopics (shown when expanded) -->
            {#if expandedTopics.has(topic.id)}
              <div class="flex flex-col items-center gap-3 w-full mt-3">
                {#each topic.subtopics as subtopic}
                  <a
                    href="/study/{subtopic.id}"
                    class="subtopic-card w-[550px] px-5 py-3 bg-gray-800 rounded-lg
                           transition-all duration-200 ease-in-out
                           hover:scale-105 hover:shadow-lg
                           focus:outline-none focus:ring-2 focus:ring-gray-400 focus:ring-offset-2
                           text-left ml-12"
                  >
                    <!-- Subtopic ID -->
                    <div class="text-xs font-bold text-white opacity-70 mb-1">
                      {subtopic.id}
                    </div>

                    <!-- Subtopic Title -->
                    <div class="text-sm font-medium text-white">
                      {subtopic.title}
                    </div>
                  </a>
                {/each}
              </div>
            {/if}
          {:else}
            <!-- Topic WITHOUT subtopics - Direct link -->
            <a
              href="/study/{topic.id}"
              class="topic-card w-[600px] px-6 py-4 bg-black rounded-xl
                     transition-all duration-200 ease-in-out
                     hover:scale-105 hover:shadow-lg
                     focus:outline-none focus:ring-2 focus:ring-gray-400 focus:ring-offset-2
                     text-left"
            >
              <!-- Topic ID -->
              <div class="text-sm font-bold text-white opacity-80 mb-1">
                {topic.id}
              </div>

              <!-- Topic Title -->
              <div class="text-base font-medium text-white">
                {topic.title}
              </div>
            </a>
          {/if}
        </div>
      {/each}
    </div>
  </main>
</div>

<style>
  /* Override any link color styling */
  a.topic-card,
  a.topic-card:visited,
  a.topic-card:hover,
  a.topic-card:active,
  a.subtopic-card,
  a.subtopic-card:visited,
  a.subtopic-card:hover,
  a.subtopic-card:active {
    color: #ffffff;
    text-decoration: none;
  }

  /* Remove default button styling */
  button.topic-card {
    border: none;
    background-color: #000000;
  }
</style>