<script>
	import { onMount } from 'svelte';
	import hljs from 'highlight.js';
	import 'highlight.js/styles/night-owl.css';

	export let code = '<div>Hello World</div>';
	export let language = 'html';

	onMount(() => {
		hljs.highlightAll();
	});
</script>

<pre class="no-prose mx-auto w-[95vw] bg-transparent md:w-[26rem] lg:w-[40rem] xl:w-full">
    <code class="language-{language} text-base">
      {@html code.replace(/</g, '&lt;').replace(/>/g, '&gt;')}
    </code>
  </pre>
