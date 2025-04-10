<script>
	import LessonLink from '../components/LessonLink.svelte';
</script>

<svelte:head>
	<title>W3b Dojo - Web Accessibility Tutorials</title>
	<meta
		name="description"
		content="Comprehensive web accessibility tutorials for beginners and intermediate developers. Learn about keyboard navigation, semantic HTML, ARIA, and more."
	/>
	<meta
		name="keywords"
		content="web accessibility, a11y, tutorials, keyboard navigation, semantic HTML, ARIA"
	/>
</svelte:head>

<section class="max-w-3xl px-2">
	<h1 class="text-4xl">Welcome to W3b Dojo!</h1>
	<h2 class="mt-8 text-2xl">What is it?</h2>
	<p class="mt-2">
		This is a set of tutorials meant for both total beginners, and intermediate developers. It is
		meant to be a comprehensive introduction to web accessibility.
	</p>
	<h2 class="mt-8 text-2xl">How does it work?</h2>
	<p class="mt-2">
		Each lesson will be composed of a brief reading section, code examples, and at the end a quiz /
		fill in the blank section. You can choose lessons in any order, as they don't build on one
		another.
	</p>
	<h2 class="mt-8 text-2xl">Contributing</h2>
	<p class="mt-2">
		If you're looking to get some experience with open-source, here's a place to do it! Whether it
		be suggestions for a new lesson or improvements to the structure of existing ones. <a
			href="https://github.com/joayo13/w3bdojo/issues">Create a new issue</a
		> and start helping today!
	</p>
	<LessonLink href="/lessons/lesson-1" text="Start Lesson 1" />
</section>
