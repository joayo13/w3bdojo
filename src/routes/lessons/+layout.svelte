<script lang="ts">
	let { children } = $props();
</script>

<section class="prose lg:prose-lg dark:prose-invert">
	{@render children()}
</section>
