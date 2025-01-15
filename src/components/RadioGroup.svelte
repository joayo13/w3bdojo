<script lang="ts">
    let { name, options, correctAnswer, isSubmitted } = $props();
  
    let selectedOption: string | null = $state(null);
  
    // Function to check if the selected answer is correct
    const isCorrect = () => selectedOption === correctAnswer;
  </script>
  
  <fieldset>
    <legend>{name}</legend>
    {#each options as option}
      <label>
        <input
          type="radio"
          name={name}
          value={option}
          bind:group={selectedOption}
        />
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