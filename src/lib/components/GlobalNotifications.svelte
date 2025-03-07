<script lang="ts">
	import { notifications } from '$lib/stores/notifications';
	import { flip } from 'svelte/animate';
	import { fade } from 'svelte/transition';
</script>

<ul
	class="fixed bottom-4 left-1/2 z-50 flex -translate-x-1/2 flex-col items-center gap-2 overflow-hidden"
>
	{#each $notifications as message (message.id)}
		<li class="w-fit rounded-lg bg-green-600 text-neutral-200 p-3 shadow-lg" transition:fade animate:flip>
			{message.message}
		</li>
	{/each}
	</ul>