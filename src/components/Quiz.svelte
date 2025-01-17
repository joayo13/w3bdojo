<script lang="ts">
	let { children, isSubmitted = $bindable() } = $props();
	function handleSubmit(e: Event) {
		e.preventDefault();
		isSubmitted = true;
	}
</script>

<h2 class="mt-8 text-4xl">Test Yourself</h2>
<form onsubmit={(e) => handleSubmit(e)}>
	{@render children()}
	<button class="submit-button mt-8" type="submit">Submit</button>
</form>
