<script lang="ts">
	import { onMount } from 'svelte';
	import '../app.css';
	import { slide } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';
	import GlobalNotifications from '$lib/components/GlobalNotifications.svelte';
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

<!-- Skip Link -->
<a
	href="#main-content"
	class="sr-only focus:not-sr-only focus:fixed focus:left-0 focus:top-0 focus:z-50 focus:bg-slate-200 focus:p-4 focus:text-slate-900 dark:focus:bg-slate-800 dark:focus:text-slate-200"
>
	Skip to main content
</a>

<nav
	class="fixed z-10 flex h-16 w-full items-center justify-between bg-slate-50 px-2 text-slate-900 shadow-sm dark:bg-slate-950 dark:text-slate-200"
>
	<span class="flex items-center gap-2">
		<img src="/logo.png" class="w-8" alt="w3b dojo logo" />
		<a href="/" class="font-mono text-xl font-bold no-underline">W3b Dojo</a>
	</span>
	<button
		onclick={toggleMobileNavLinks}
		class="flex h-10 w-10 flex-col justify-evenly md:hidden"
		aria-label="hamburger"
	>
		<div class="h-1 w-full rounded-full bg-slate-900 dark:bg-slate-200"></div>
		<div class="h-1 w-3/4 rounded-full bg-slate-900 dark:bg-slate-200"></div>
		<div class="h-1 w-full rounded-full bg-slate-900 dark:bg-slate-200"></div>
	</button>
</nav>
<!-- desktop nav links -->
<nav
	aria-labelledby="lessons-header"
	class="fixed hidden h-screen w-80 flex-col bg-slate-200 px-4 pt-16 text-right text-slate-900 lg:flex dark:bg-slate-800 dark:text-slate-200"
>
	<h2 class="mt-14 text-2xl font-bold" id="lessons-header">Lessons</h2>
	<ul class="relative mt-8 flex flex-col gap-8">
		<li>
			<a href="/lessons/lesson-1">Keyboard Accessibility</a>
		</li>
		<li>
			<a href="/lessons/lesson-2">Skip Links and Tab-Index</a>
		</li>
		<li>
			<a href="/lessons/lesson-3">ARIA 101</a>
		</li>
		<li>
			<a href="/lessons/lesson-4">Testing Accessibility</a>
		</li>
		<li>
			<a href="/lessons/lesson-5">Visual Accessibility</a>
		</li>
		<li>
			<div aria-hidden="true" class="h-px w-full bg-slate-900 dark:bg-slate-200"></div>
			<button
				onclick={toggleDarkMode}
				aria-label="Toggle dark mode"
				aria-pressed={darkMode}
				class="relative ml-auto mt-8 h-8 w-16 rounded-full border border-slate-900 dark:border-slate-200"
			>
				<div
					class="absolute right-0 top-1/2 size-8 -translate-y-1/2 bg-moon-svg dark:left-0 dark:bg-sun-svg"
				></div>
			</button>
		</li>
	</ul>
</nav>
<!-- /desktop nav links -->
<!-- mobile nav links -->
{#if mobileNavLinksVisible}
	<nav
		aria-labelledby="lessons-header"
		transition:slide={{ delay: 100, duration: 300, easing: quintOut, axis: 'x' }}
		class="fixed right-0 z-10 h-screen w-80 flex-col whitespace-nowrap bg-slate-200 px-4 text-left text-neutral-900 dark:bg-slate-800 dark:text-neutral-200"
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
		<h2 class="mt-14 text-2xl font-bold" id="lessons-header">Lessons</h2>
		<ul class="mt-8 flex flex-col gap-8">
			<li>
				<a onclick={toggleMobileNavLinks} href="/lessons/lesson-1">Keyboard Accessibility</a>
			</li>
			<li>
				<a onclick={toggleMobileNavLinks} href="/lessons/lesson-2">Skip Links And Tab-Index</a>
			</li>
			<li>
				<a onclick={toggleMobileNavLinks} href="/lessons/lesson-3">ARIA 101</a>
			</li>
			<li>
				<a onclick={toggleMobileNavLinks} href="/lessons/lesson-4">Testing Accessibility</a>
			</li>
			<li>
				<a onclick={toggleMobileNavLinks} href="/lessons/lesson-5">Visual Accessibility</a>
			</li>
			<div class="h-px w-full bg-slate-900 dark:bg-slate-200"></div>
			<button
				onclick={toggleDarkMode}
				aria-label="Toggle dark mode"
				aria-pressed={darkMode}
				class="relative h-8 w-16 rounded-full border border-slate-900 dark:border-slate-200"
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
	id="main-content"
	class="flex min-h-screen justify-center bg-slate-100 px-2 pt-32 text-lg text-neutral-900 lg:pl-80 dark:bg-slate-900 dark:text-neutral-200"
>
	<GlobalNotifications />
	{@render children()}
</div>
<footer
	class="bg-slate-50 py-8 text-slate-900 shadow-sm lg:pl-80 dark:bg-slate-950 dark:text-slate-200"
>
	<div class="mx-auto max-w-3xl px-2">
		<p>© 2025 W3b Dojo. All rights reserved.</p>
		<a href="https://www.flaticon.com/free-icons/japan" title="japan icons"
			>Japan icons created by Freepik - Flaticon</a
		>
	</div>
</footer>
