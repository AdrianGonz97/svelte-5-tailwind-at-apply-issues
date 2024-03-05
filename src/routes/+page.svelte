<script>
	import { untrack } from "svelte";

	let isDark = $state();

	$effect(() => {
		untrack(
			() => (isDark = document.documentElement.classList.contains("dark"))
		);
	});

	function toggleTheme() {
		isDark = !isDark;
		document.documentElement.classList.toggle("dark", isDark);
	}
</script>

<main class="grid h-[100vh]">
	<!-- utility classes defined inline work -->
	<div class="dark:bg-blue-900 bg-blue-100 grid place-items-center">
		<button onclick={toggleTheme} class="size-12 bg-black">
			{isDark ? "☀️" : "🌙"}
		</button>
	</div>
	<div class="foo grid place-items-center">
		<button onclick={toggleTheme} class="size-12 bg-black">
			{isDark ? "☀️" : "🌙"}
		</button>
	</div>
</main>

<style lang="postcss">
	/* utility classes defined with @apply DO NOT work */
	.foo {
		@apply dark:bg-red-900 bg-red-100;
	}
</style>
