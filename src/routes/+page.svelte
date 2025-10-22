<script lang="ts">
	import { resolve } from '$app/paths';

	const domainsHref = resolve('/domains');
</script>

<!--
  CCNA Study Website - Home Page
  Black and white color scheme optimized for studying
-->

<div class="flex min-h-screen flex-col bg-white">
	<!-- Navigation Bar -->
	<nav class="w-full border-b border-gray-200 px-6 py-4">
		<div class="mx-auto max-w-7xl">
			<h1 class="text-2xl font-bold text-black">CCNA Study Guide</h1>
		</div>
	</nav>

	<!-- Main Content Area - Centered vertically and horizontally -->
	<main class="flex flex-1 items-center justify-center px-6">
		<div class="text-center">
			<!-- Main Call-to-Action Button -->
			<a
				href={domainsHref}
				class="inline-block rounded-lg bg-black px-8 py-4 text-lg font-semibold text-white
               transition-all duration-200 ease-in-out
               hover:scale-105 hover:shadow-lg
               focus:ring-2 focus:ring-gray-400 focus:ring-offset-2 focus:outline-none"
			>
				CCNA 200-301 v1.1
			</a>
		</div>
	</main>
</div>

<style>
	/* Additional styles if needed - TailwindCSS handles most styling */
	:global(body) {
		font-family:
			-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
		margin: 0;
		padding: 0;
	}
</style>
