<script lang="ts">
	import '../app.css';
	let { children } = $props();
</script>

<nav class="fixed bg-neutral-900 h-16 w-full z-10">
	
</nav>
<nav aria-labelledby="lessons-header" class="hidden md:flex flex-col fixed w-80 pt-16 px-2 bg-neutral-200 h-screen">
	<h2 class="text-xl" id="lessons-header">Lessons</h2>
	<ul class="flex flex-col gap-2">
		<li>
			<a href="/">Home</a>
		</li>
	</ul>
</nav>
<div class="md:pl-80 pt-16 bg-neutral-50 text-neutral-900 flex justify-center">
{@render children()}
</div>

