<script lang="ts">
	import '../app.css';
	import DarkModeButton from '../components/DarkModeButton.svelte';
	import LightModeButton from '../components/LightModeButton.svelte';
	let darkMode = $state(false);
	let { children } = $props();

	function toggleMode() {
		darkMode = !darkMode;
	}
</script>

<nav class="fixed z-10 h-16 w-full bg-neutral-900">
	{#if darkMode === true}
		<DarkModeButton {toggleMode} />
	{:else}
		<LightModeButton {toggleMode} />
	{/if}
</nav>
<nav
	aria-labelledby="lessons-header"
	class="fixed hidden h-screen w-80 flex-col bg-neutral-200 px-2 pt-16 text-right md:flex"
>
	<h2 class="mt-16 text-2xl" id="lessons-header">Lessons</h2>
	<ul class="mt-8 flex flex-col gap-8 text-xl">
		<li>
			<a href="/lesson-1">Lesson 1: Keyboard Accessibility</a>
		</li>
		<li>
			<a href="/lesson-1">Lesson 2: ARIA 101</a>
		</li>
	</ul>
</nav>
<div class="flex justify-center bg-neutral-50 pt-32 text-neutral-900 md:pl-80">
	{@render children()}
</div>
