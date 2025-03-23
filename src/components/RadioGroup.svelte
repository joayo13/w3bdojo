<script lang="ts">
	import { getContext, onMount } from 'svelte';
	import type { QuizContext } from '../types';

	let { name, options, correctAnswer } = $props();

	let isIncorrect = $state(true);

	let selectedOption: string | null = $state(null);

	const normalFieldsetStyle =
		'mt-12 flex flex-col gap-4 rounded-lg border border-slate-900 bg-slate-300 py-4 px-6 dark:border-slate-200 dark:bg-slate-950';

	const correctFieldsetStyle =
		'mt-12 flex flex-col gap-4 rounded-lg border border-slate-900 bg-green-300 py-4 px-6 dark:border-slate-200 dark:bg-green-700';

	const { incrementCount, incrementCorrect, decrementCorrect } =
		getContext<QuizContext>('incrementCount');

	const isSubmitted: () => boolean = getContext('isSubmitted');
	// Function to check if the selected answer is correct
	onMount(() => {
		incrementCount();
	});
	function evaluateAnswer() {
		if (correctAnswer === selectedOption) {
			incrementCorrect();
			isIncorrect = false;
		} else if (!isIncorrect) {
			decrementCorrect();
			isIncorrect = true;
		}
	}
</script>

<fieldset
	class={isSubmitted() && selectedOption === correctAnswer
		? correctFieldsetStyle
		: normalFieldsetStyle}
>
	<legend class="text-2xl font-bold">{name}</legend>
	{#each options as option}
		<label>
			<input
				type="radio"
				required
				{name}
				value={option}
				bind:group={selectedOption}
				onchange={evaluateAnswer}
			/>
			{option}
		</label>
	{/each}
</fieldset>
