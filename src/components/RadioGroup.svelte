<script lang="ts">
	let { name, options, correctAnswer, isSubmitted } = $props();

	let selectedOption: string | null = $state(null);

	// Function to check if the selected answer is correct
	const isCorrect = () => selectedOption === correctAnswer;
	function displayCorrectOrIncorrectStyle() {
		if(correctAnswer && isSubmitted) {
			"backgroundColor: green;"
		}
		else if(!correctAnswer && isSubmitted) {
			"backgroundColor: red;"
		}
	}
</script>

<fieldset class="rounded-md bg-neutral-300 dark:bg-neutral-950 border-neutral-900 dark:border-neutral-200  mt-12 flex flex-col gap-4 border p-4">
	<legend class="text-2xl font-bold">{name}</legend>
	{#each options as option}
		<label>
			<input type="radio" required {name} value={option} bind:group={selectedOption} />
			{option}
		</label>
	{/each}
</fieldset>

{#if isSubmitted}
	<p>
		{selectedOption
			? `You selected: ${selectedOption} (${isCorrect() ? 'Correct' : 'Incorrect'})`
			: 'No selection made'}
	</p>
{/if}
