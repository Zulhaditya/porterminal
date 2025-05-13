<script>
  export let outputHistory = [];
</script>

<div class="output-display">
  {#each outputHistory as output}
    <div class="output-line">{@html output}</div>
  {/each}
</div>

<style>
  .output-display {
    flex: 1;
    overflow-y: auto;
    margin-bottom: 10px;
  }

  .output-line {
    margin-bottom: 8px;
    line-height: 1.4;
    white-space: pre-wrap;
  }
</style>
