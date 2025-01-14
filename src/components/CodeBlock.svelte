<script>
    import { onMount } from "svelte";
    import hljs from "highlight.js";
    import "highlight.js/styles/github-dark.css";
  
    export let code = "<div>Hello World</div>";
    export let language = "html";
  
    onMount(() => {
      hljs.highlightAll();
    });
  </script>
  
  <pre>
    <code class="language-{language} text-base">
      {@html code.replace(/</g, '&lt;').replace(/>/g, '&gt;')}
    </code>
  </pre>