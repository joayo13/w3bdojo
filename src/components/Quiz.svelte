<script lang="ts">
	import { setContext } from 'svelte';
	import type { QuizContext } from '../types';

	let { children } = $props();
	let isSubmitted = $state(false);
	let count = $state({
		total: 0,
		correct: 0
	});
	function round(value: number, precision: number) {
		const multiplier = Math.pow(10, precision || 0);
		return Math.round(value * multiplier) / multiplier;
	}
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
	function decrementCorrect() {
		count.correct -= 1;
	}
	setContext<QuizContext>('incrementCount', {
		incrementCount,
		incrementCorrect,
		decrementCorrect
	});
	setContext('isSubmitted', () => isSubmitted);
</script>

<h2 class="mt-8 text-4xl">Test Yourself</h2>
<form onsubmit={(e) => handleSubmit(e)}>
	{@render children()}
	<button class="submit-button mt-8" type="submit">Submit</button>
</form>
{#if isSubmitted}
	<p class="mt-8">
		You scored {count.correct} / {count.total} ({round((count.correct / count.total) * 100, 1)}%)
	</p>
{/if}
