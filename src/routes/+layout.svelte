<script lang="ts">
	import '../app.css';
	let { children } = $props();
</script>

<nav class="fixed bg-neutral-900 h-16 w-full z-10">
	
</nav>
<nav aria-labelledby="lessons-header" class="hidden md:flex flex-col fixed w-80 h-screen pt-16 px-2 bg-neutral-200 text-right">
	<h2 class="text-2xl mt-16" id="lessons-header">Lessons</h2>
	<ul class="flex flex-col gap-8 text-xl mt-8">
		<li>
			<a href="/lesson-1">Lesson 1: Keyboard Accessibility</a>
		</li>
		<li>
			<a href="/lesson-1">Lesson 2: ARIA 101</a>
		</li>
	</ul>
</nav>
<div class="md:pl-80 pt-32 bg-neutral-50 text-neutral-900 flex justify-center">
{@render children()}
</div>

