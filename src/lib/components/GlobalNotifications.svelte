<script lang="ts">
	import { notifications } from '$lib/stores/notifications';
	import { fade } from 'svelte/transition';
</script>

<ul
	class="fixed bottom-4 left-1/2 z-50 flex -translate-x-1/2 flex-col items-center gap-2 overflow-hidden"
>
	{#each $notifications as message (message.id)}
		<li
			class="w-fit rounded-lg border border-slate-900 bg-slate-200 p-3 dark:border-slate-200 dark:bg-slate-800"
			transition:fade={{ duration: 300 }}
		>
			{message.message}
		</li>
	{/each}
</ul>
