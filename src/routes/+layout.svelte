<script lang="ts">
	import { onMount } from 'svelte';
	import '../app.css';
	import { slide } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	let darkMode = $state(false);
	let mobileNavLinksVisible = $state(false);
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
	function toggleMobileNavLinks() {
		mobileNavLinksVisible = !mobileNavLinksVisible
		document.body.classList.toggle('no-doc-scroll')
	}

</script>

<nav class="fixed flex items-center justify-between shadow-sm z-10 h-16 w-full px-2 bg-neutral-50 dark:bg-neutral-950 text-neutral-900 dark:text-neutral-200">
	<a href="/" class="text-xl no-underline font-bold">W.A.I.T</a>
	<button onclick={toggleMobileNavLinks} class="h-10 w-10 flex md:hidden flex-col justify-evenly" aria-label="hamburger">
		<div class="h-1 w-full bg-neutral-900 dark:bg-neutral-200"></div>
		<div class="h-1 w-3/4 bg-neutral-900 dark:bg-neutral-200"></div>
		<div class="h-1 w-full bg-neutral-900 dark:bg-neutral-200"></div>
	</button>
</nav>
<!-- desktop nav links -->
<nav
	aria-labelledby="lessons-header"
	class="fixed w-80 hidden h-screen flex-col bg-neutral-200 dark:bg-neutral-800 text-neutral-900 dark:text-neutral-200 px-4 pt-16 text-right md:flex"
>
	<h2 class="mt-14 text-2xl" id="lessons-header">Lessons</h2>
	<ul class="mt-8 flex flex-col gap-8 text-xl">
		<li>
			<a href="/lesson-1">Lesson 0: Introduction</a>
		</li>
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
	<button onclick={toggleDarkMode} aria-label="Toggle dark mode" aria-pressed={darkMode} class="bg-moon-svg dark:bg-sun-svg size-10"></button>
</nav>
<!-- /desktop nav links -->
 <!-- mobile nav links -->
{#if mobileNavLinksVisible}
 <nav
 aria-labelledby="lessons-header"
 transition:slide={{ delay: 100, duration: 300, easing: quintOut, axis: 'x' }}
 class="fixed right-0  whitespace-nowrap h-screen w-80 flex-col bg-neutral-200 dark:bg-neutral-800 text-neutral-900 dark:text-neutral-200 px-4 pt-16 text-left"
>
 <h2 class="mt-14 text-2xl" id="lessons-header">Lessons</h2>
 <ul class="mt-8 flex flex-col gap-8 text-xl">
	 <li>
		 <a href="/lesson-1">Lesson 0: Introduction</a>
	 </li>
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
 <button onclick={toggleDarkMode} aria-label="Toggle dark mode" aria-pressed={darkMode} class="bg-moon-svg dark:bg-sun-svg size-10"></button>
</nav>
{/if}
 <!-- /mobile nav links -->

<div class="flex justify-center bg-neutral-100 dark:bg-neutral-900 pt-32 text-neutral-900 dark:text-neutral-200 min-h-screen md:pl-80">
	{@render children()}
</div>
