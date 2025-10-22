<script lang="ts">
  /**
   * Domain 4.0 - IP Services Detail Page
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

  // Domain 4.0 Topics (from official CCNA 200-301 v1.1 blueprint)
  const topics: Topic[] = [
    {
      id: '4.1',
      title: 'Configure and verify inside source NAT using static and pools'
    },
    {
      id: '4.2',
      title: 'Configure and verify NTP operating in a client and server mode'
    },
    {
      id: '4.3',
      title: 'Explain the role of DHCP and DNS within the network'
    },
    {
      id: '4.4',
      title: 'Explain the function of SNMP in network operations'
    },
    {
      id: '4.5',
      title: 'Describe the use of syslog features, including facilities and severity levels'
    },
    {
      id: '4.6',
      title: 'Configure and verify DHCP client and relay'
    },
    {
      id: '4.7',
      title: 'Explain the forwarding per-hop behavior (PHB) for QoS such as classification, marking, queuing, congestion, policing, and shaping'
    },
    {
      id: '4.8',
      title: 'Configure network devices for remote access using SSH'
    },
    {
      id: '4.9',
      title: 'Describe the capabilities and functions of TFTP/FTP in the network'
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
      <h1 class="text-4xl font-bold text-black mb-2">Domain 4.0 - IP Services</h1>
      <p class="text-xl text-gray-600">10% of exam</p>
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