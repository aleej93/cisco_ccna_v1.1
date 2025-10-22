<script lang="ts">
  /**
   * Domain 6.0 - Automation and Programmability Detail Page
   * Lists all topics within this domain (no subtopics)
   */

  interface Subtopic {
    id: string;
    title: string;
  }

  interface Topic {
    id: string;
    title: string;
    subtopics?: Subtopic[];
  }

  let expandedTopics: Set<string> = new Set();

  function toggleTopic(topicId: string) {
    if (expandedTopics.has(topicId)) {
      expandedTopics.delete(topicId);
    } else {
      expandedTopics.add(topicId);
    }
    expandedTopics = expandedTopics;
  }

  const topics: Topic[] = [
    { id: '6.1', title: 'Explain how automation impacts network management' },
    { id: '6.2', title: 'Compare traditional networks with controller-based networking' },
    {
      id: '6.3',
      title:
        'Describe controller-based, software defined architecture (overlay, underlay, and fabric; separation of control plane and data plane; northbound and southbound APIs)'
    },
    {
      id: '6.4',
      title: 'Explain AI (generative and predictive) and machine learning in network operations'
    },
    {
      id: '6.5',
      title:
        'Describe characteristics of REST-based APIs (authentication types, CRUD, HTTP verbs, and data encoding)'
    },
    {
      id: '6.6',
      title: 'Recognize the capabilities of configuration management mechanisms such as Ansible and Terraform'
    },
    { id: '6.7', title: 'Recognize components of JSON-encoded data' }
  ];
</script>

<div class="min-h-screen bg-white">
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

  <main class="flex flex-col items-center justify-center px-6 py-16">
    <div class="text-center mb-12">
      <h1 class="text-4xl font-bold text-black mb-2">Domain 6.0 - Automation and Programmability</h1>
      <p class="text-xl text-gray-600">10% of exam</p>
    </div>

    <div class="w-full max-w-[600px] mb-6">
      <h2 class="text-2xl font-bold text-black">Topics</h2>
    </div>

    <div class="flex flex-col items-center gap-4 w-full">
      {#each topics as topic}
        <div class="flex flex-col items-center w-full">
          {#if topic.subtopics && topic.subtopics.length > 0}
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
                  <div class="text-sm font-bold text-white opacity-80 mb-1">
                    {topic.id}
                  </div>
                  <div class="text-base font-medium text-white">
                    {topic.title}
                  </div>
                </div>
                <div class="text-white text-xl ml-4 flex-shrink-0">
                  {expandedTopics.has(topic.id) ? '▲' : '▼'}
                </div>
              </div>
            </button>

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
                    <div class="text-xs font-bold text-white opacity-70 mb-1">
                      {subtopic.id}
                    </div>
                    <div class="text-sm font-medium text-white">
                      {subtopic.title}
                    </div>
                  </a>
                {/each}
              </div>
            {/if}
          {:else}
            <a
              href="/study/{topic.id}"
              class="topic-card w-[600px] px-6 py-4 bg-black rounded-xl
                     transition-all duration-200 ease-in-out
                     hover:scale-105 hover:shadow-lg
                     focus:outline-none focus:ring-2 focus:ring-gray-400 focus:ring-offset-2
                     text-left"
            >
              <div class="text-sm font-bold text-white opacity-80 mb-1">
                {topic.id}
              </div>
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

  button.topic-card {
    border: none;
    background-color: #000000;
  }
</style>
