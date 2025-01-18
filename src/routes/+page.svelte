<script>
	import LessonLink from '../components/LessonLink.svelte';
</script>

<section class="max-w-3xl px-2">
	<h1 class="text-4xl">Web Accessibility Interactive Tutorial</h1>
	<h2 class="mt-8 text-2xl">Who is this tutorial for?</h2>
	<p class="mt-2">
		This tutorial is meant for both total beginners, and intermediate developers. It is meant to be
		a comprehensive introduction to accessibility.
	</p>
	<h2 class="mt-8 text-2xl">How does it work?</h2>
	<p class="mt-2">
		Each lesson will be composed of a brief reading section, code examples, and at the end a quiz /
		fill in the blank section. You can choose lessons in any order, as they don’t build on one
		another. However, it is recommended that you start at the beginning and work your way through.
	</p>
	<h2 class="mt-8 text-2xl">Contributing</h2>
	<p class="mt-2">
		If you're looking to get some experience with open-source, here's a place to do it! Whether it
		be suggestions for a new lesson or improvements to the structure of existing ones. <a
			href="https://github.com/joayo13/wait/issues">Create a new issue</a
		> and start helping today!
	</p>
	<LessonLink href="/lessons/lesson-1" text="Start Lesson 1" />
</section>
