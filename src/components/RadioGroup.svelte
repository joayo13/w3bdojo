<script lang="ts">
	import { getContext, onMount } from 'svelte';
	import type { QuizContext } from '../types';

	let { name, options, correctAnswer } = $props();

	let isIncorrect = $state(true);

	let selectedOption: string | null = $state(null);

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

<fieldset class="mt-4 flex flex-col gap-4">
	<legend><h3>{name}</h3></legend>
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
	{#if isSubmitted() && correctAnswer === selectedOption}
		<div class="flex items-center gap-2">
			<svg
				xmlns="http://www.w3.org/2000/svg"
				viewBox="0 0 24 24"
				fill="currentColor"
				class="inline-block size-6"
			>
				<path
					fill-rule="evenodd"
					d="M2.25 12c0-5.385 4.365-9.75 9.75-9.75s9.75 4.365 9.75 9.75-4.365 9.75-9.75 9.75S2.25 17.385 2.25 12Zm13.36-1.814a.75.75 0 1 0-1.22-.872l-3.236 4.53L9.53 12.22a.75.75 0 0 0-1.06 1.06l2.25 2.25a.75.75 0 0 0 1.14-.094l3.75-5.25Z"
					clip-rule="evenodd"
				/>
			</svg>
			<p>Correct!</p>
		</div>
	{/if}
	{#if isSubmitted() && correctAnswer !== selectedOption}
		<div class="flex items-center gap-2">
			<svg
				xmlns="http://www.w3.org/2000/svg"
				viewBox="0 0 24 24"
				fill="currentColor"
				class="size-6"
			>
				<path
					fill-rule="evenodd"
					d="M12 2.25c-5.385 0-9.75 4.365-9.75 9.75s4.365 9.75 9.75 9.75 9.75-4.365 9.75-9.75S17.385 2.25 12 2.25Zm-1.72 6.97a.75.75 0 1 0-1.06 1.06L10.94 12l-1.72 1.72a.75.75 0 1 0 1.06 1.06L12 13.06l1.72 1.72a.75.75 0 1 0 1.06-1.06L13.06 12l1.72-1.72a.75.75 0 1 0-1.06-1.06L12 10.94l-1.72-1.72Z"
					clip-rule="evenodd"
				/>
			</svg>
			<p>Incorrect: Correct answer is {correctAnswer}</p>
		</div>
	{/if}
</fieldset>
