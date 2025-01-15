<script lang="ts">
    let { children, isSubmitted = $bindable() } = $props();
    function handleSubmit(e: Event) {
        e.preventDefault();
        isSubmitted = true
    }
      
  </script>
  
  <form onsubmit={(e) => handleSubmit(e)}>
    {@render children()}
    <button type="submit">Submit</button>
  </form>