<script lang="ts">
	import { onMount } from 'svelte';
	import '../app.css';
	let darkMode = $state(false);
	let { children } = $props();


	onMount(() => {
		if(localStorage.getItem("theme") === "dark") {
			darkMode = true
		}
		if(localStorage.getItem("theme") === "light") {
			darkMode = false
		}
	})

	function toggleDarkMode() {
		
		if (darkMode === true) {
			localStorage.setItem("theme", "light")
			document.documentElement.classList.remove('dark')
			darkMode = false
		}
		else {
			localStorage.setItem("theme", "dark");
			document.documentElement.classList.add('dark')
			darkMode = true
		}
		

	}
</script>

<nav class="fixed flex items-center justify-between shadow-sm z-10 h-16 w-full px-2 bg-neutral-50 dark:bg-neutral-950 text-neutral-900 dark:text-neutral-200">
	<a href="/" class="text-xl no-underline">W.A.I.T</a>
	<button onclick={toggleDarkMode} aria-label="Toggle dark mode" aria-pressed={darkMode} class="bg-moon-svg dark:bg-sun-svg size-10"></button>
</nav>
<nav
	aria-labelledby="lessons-header"
	class="fixed hidden h-screen w-80 flex-col bg-neutral-200 dark:bg-neutral-800 text-neutral-900 dark:text-neutral-200 px-4 pt-16 text-right md:flex"
>
	<h2 class="mt-14 text-2xl" id="lessons-header">Lessons</h2>
	<ul class="mt-8 flex flex-col gap-8 text-xl">
		<li>
			<a href="/lesson-1">Lesson 1: Keyboard Accessibility</a>
		</li>
		<li>
			<a href="/lesson-1">Lesson 2: ARIA 101</a>
		</li>
		<li>
			<a href="/lesson-1">Lesson 3: REMS</a>
		</li>
	</ul>
</nav>
<div class="flex justify-center bg-neutral-100 dark:bg-neutral-900 pt-32 text-neutral-900 dark:text-neutral-200 min-h-screen md:pl-80">
	{@render children()}
</div>
