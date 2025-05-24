<script lang="ts">
	let { children } = $props();
</script>

<section class="prose lg:prose-xl dark:prose-invert">
	{@render children()}
</section>
