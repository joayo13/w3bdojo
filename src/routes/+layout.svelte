<script lang="ts">
	import { onMount } from 'svelte';
	import '../app.css';
	import { slide } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	let darkMode = $state(false);
	let mobileNavLinksVisible = $state(false);
	let { children } = $props();

	onMount(() => {
		if (localStorage.getItem('theme') === 'dark') {
			darkMode = true;
		}
		if (localStorage.getItem('theme') === 'light') {
			darkMode = false;
		}
	});

	function toggleDarkMode() {
		if (darkMode === true) {
			localStorage.setItem('theme', 'light');
			document.documentElement.classList.remove('dark');
			darkMode = false;
		} else {
			localStorage.setItem('theme', 'dark');
			document.documentElement.classList.add('dark');
			darkMode = true;
		}
	}
	function toggleMobileNavLinks() {
		mobileNavLinksVisible = !mobileNavLinksVisible;
		document.body.classList.toggle('no-doc-scroll');
	}
</script>

<nav
	class="fixed z-10 flex h-16 w-full items-center justify-between bg-neutral-50 px-2 text-neutral-900 shadow-sm dark:bg-neutral-950 dark:text-neutral-200"
>
	<a href="/" class="text-xl font-bold no-underline">W.A.I.T</a>
	<button
		onclick={toggleMobileNavLinks}
		class="flex h-10 w-10 flex-col justify-evenly md:hidden"
		aria-label="hamburger"
	>
		<div class="h-1 w-full bg-neutral-900 dark:bg-neutral-200"></div>
		<div class="h-1 w-3/4 bg-neutral-900 dark:bg-neutral-200"></div>
		<div class="h-1 w-full bg-neutral-900 dark:bg-neutral-200"></div>
	</button>
</nav>
<!-- desktop nav links -->
<nav
	aria-labelledby="lessons-header"
	class="fixed hidden h-screen w-80 flex-col bg-neutral-200 px-4 pt-16 text-right text-neutral-900 md:flex dark:bg-neutral-800 dark:text-neutral-200"
>
	<h2 class="mt-14 text-2xl" id="lessons-header">Lessons</h2>
	<ul class="relative mt-8 flex flex-col gap-8 text-xl">
		<li>
			<a href="/lessons/lesson-1">Lesson 1: Keyboard Accessibility</a>
		</li>
		<li>
			<a href="/lessons/lesson-2">Lesson 2: ARIA 101</a>
		</li>
		<li>
			<a href="/lessons/lesson-3">Lesson 3: REMS</a>
		</li>
		<div class="h-px w-full bg-neutral-900 dark:bg-neutral-200"></div>
		<button
			onclick={toggleDarkMode}
			aria-label="Toggle dark mode"
			aria-pressed={darkMode}
			class="relative ml-auto h-8 w-16 rounded-full border border-neutral-900 dark:border-neutral-200"
		>
			<div
				class="absolute right-0 top-1/2 size-8 -translate-y-1/2 bg-moon-svg dark:left-0 dark:bg-sun-svg"
			></div>
		</button>
	</ul>
</nav>
<!-- /desktop nav links -->
<!-- mobile nav links -->
{#if mobileNavLinksVisible}
	<nav
		aria-labelledby="lessons-header"
		transition:slide={{ delay: 100, duration: 300, easing: quintOut, axis: 'x' }}
		class="fixed right-0 z-10 h-screen w-80 flex-col whitespace-nowrap bg-neutral-200 px-4 text-left text-neutral-900 dark:bg-neutral-800 dark:text-neutral-200"
	>
		<button
			class="absolute right-2 top-2"
			aria-label="exit-hamburger"
			onclick={toggleMobileNavLinks}
		>
			<svg
				xmlns="http://www.w3.org/2000/svg"
				fill="none"
				viewBox="0 0 24 24"
				stroke-width="2"
				stroke="currentColor"
				class="size-12"
			>
				<path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
			</svg>
		</button>
		<h2 class="mt-14 text-2xl" id="lessons-header">Lessons</h2>
		<ul class="mt-8 flex flex-col gap-8 text-xl">
			<li>
				<a href="/lessons/lesson-1">Lesson 1: Keyboard Accessibility</a>
			</li>
			<li>
				<a href="/lessons/lesson-2">Lesson 2: ARIA 101</a>
			</li>
			<li>
				<a href="/lessons/lesson-3">Lesson 3: REMS</a>
			</li>
			<div class="h-px w-full bg-neutral-900 dark:bg-neutral-200"></div>
			<button
				onclick={toggleDarkMode}
				aria-label="Toggle dark mode"
				aria-pressed={darkMode}
				class="relative h-8 w-16 rounded-full border border-neutral-900 dark:border-neutral-200"
			>
				<div
					class="absolute right-0 top-1/2 size-8 -translate-y-1/2 bg-moon-svg dark:left-0 dark:bg-sun-svg"
				></div>
			</button>
		</ul>
	</nav>
{/if}
<!-- /mobile nav links -->

<div
	class="flex min-h-screen justify-center bg-neutral-100 pt-32 text-xl text-neutral-900 md:pl-80 dark:bg-neutral-900 dark:text-neutral-200"
>
	{@render children()}
</div>
