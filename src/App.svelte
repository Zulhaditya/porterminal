<script>
  import Terminal from "./lib/Terminal.svelte";
</script>

<main>
  <div class="header">
    <h1>Terminal Portfolio</h1>
    <p>Navigate using commands. Type "help" to begin.</p>
  </div>
  <Terminal />
</main>

<style>
  :global(#app) {
    text-align: left !important;
  }
  :global(body) {
    margin: 0;
    padding: 0;
    background-color: #000;
    color: #00ff00;
    font-family: "Courier New", monospace;
  }

  .header {
    text-align: center;
    margin-bottom: 1.5rem;
  }

  h1 {
    color: #00ff00;
    font-size: 2rem;
    margin-bottom: 0.5rem;
  }

  p {
    color: #00aa00;
    margin-top: 0;
  }
</style>
