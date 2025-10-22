<script lang="ts">
  /**
   * CCNA Exam Domains List Page
   * Displays all 6 CCNA 200-301 v1.1 exam domains
   */

  // TypeScript interface for domain data structure
  interface Domain {
    id: number;
    number: string;
    name: string;
    percentage: number;
  }

  // CCNA 200-301 v1.1 Exam Domains
  const domains: Domain[] = [
    {
      id: 1,
      number: '1.0',
      name: 'Network Fundamentals',
      percentage: 20
    },
    {
      id: 2,
      number: '2.0',
      name: 'Network Access',
      percentage: 20
    },
    {
      id: 3,
      number: '3.0',
      name: 'IP Connectivity',
      percentage: 25
    },
    {
      id: 4,
      number: '4.0',
      name: 'IP Services',
      percentage: 10
    },
    {
      id: 5,
      number: '5.0',
      name: 'Security Fundamentals',
      percentage: 15
    },
    {
      id: 6,
      number: '6.0',
      name: 'Automation and Programmability',
      percentage: 10
    }
  ];
</script>

<div class="min-h-screen bg-white">
  <!-- Navigation Bar with Back Button -->
  <nav class="w-full border-b border-gray-200 px-6 py-4">
    <div class="max-w-7xl mx-auto">
      <a
        href="/"
        class="inline-flex items-center text-black hover:text-gray-600 transition-colors duration-200"
      >
        <span class="text-lg">←</span>
        <span class="ml-2 font-medium">Back to Home</span>
      </a>
    </div>
  </nav>

  <!-- Main Content -->
  <main class="flex flex-col items-center justify-center px-6 py-16">
    <!-- Page Title - Centered -->
    <div class="text-center mb-12">
      <h1 class="text-4xl font-bold text-black mb-2">CCNA 200-301 v1.1</h1>
      <p class="text-xl text-gray-600">Exam Domains</p>
    </div>

    <!-- Domain Cards - Centered Vertical Stack -->
    <div class="flex flex-col items-center gap-6 w-full">
      {#each domains as domain}
        <a
          href="/domains/{domain.id}"
          class="domain-card w-[650px] px-8 py-6 bg-black rounded-xl
                 transition-all duration-200 ease-in-out
                 hover:scale-105 hover:shadow-lg
                 focus:outline-none focus:ring-2 focus:ring-gray-400 focus:ring-offset-2
                 text-center"
        >
          <!-- Domain Number (Bold) -->
          <div class="text-xs font-bold text-white opacity-80 mb-1">
            Domain {domain.number}
          </div>

          <!-- Domain Name (Larger) -->
          <div class="text-lg font-semibold text-white mb-1 whitespace-nowrap">
            {domain.name}
          </div>

          <!-- Domain Percentage -->
          <div class="text-sm text-white opacity-80">
            {domain.percentage}% of exam
          </div>
        </a>
      {/each}
    </div>
  </main>
</div>

<style>
  /* Override any link color styling */
  a.domain-card,
  a.domain-card:visited,
  a.domain-card:hover,
  a.domain-card:active {
    color: #ffffff;
    text-decoration: none;
  }
</style>
