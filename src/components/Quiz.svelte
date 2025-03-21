<script lang="ts">
	import { setContext } from 'svelte';
	import type { QuizContext } from '../types';

	let { children } = $props();
	let isSubmitted = $state(false);
	let count = $state({
		total: 0,
		correct: 0
	});

	function handleSubmit(e: Event) {
		e.preventDefault();
		isSubmitted = true;
	}
	function incrementCount() {
		count.total += 1;
	}
	function incrementCorrect() {
		count.correct += 1;
	}
	setContext<QuizContext>('incrementCount', {
		incrementCount,
		incrementCorrect
	});
</script>

<h2 class="mt-8 text-4xl">Test Yourself</h2>
{count.total + ' ' + count.correct}
<form onsubmit={(e) => handleSubmit(e)}>
	{@render children()}
	<button class="submit-button mt-8" type="submit">Submit</button>
</form>
