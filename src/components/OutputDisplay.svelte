<script>
  export let outputHistory = [];
  export let commandHistory = [];
  let outputContainer;

  // autoscroll when outputHistory changed
  $: if (outputContainer) {
    outputContainer.scrollTop = outputContainer.scrollHeight;
  }
</script>

<div class="output-container" bind:this={outputContainer}>
  {#each outputHistory as output, i}
    <div class="output-line">
      {#if commandHistory[i]?.startsWith("calc ")}
        <span class="prompt">$</span>
        {commandHistory[i]}
        <div class="math-result">{output}</div>
      {:else}
        {@html output}
      {/if}
    </div>
  {/each}
</div>

<style>
  .output-container {
    flex: 1;
    overflow-y: auto;
    padding-right: 10px;
    scroll-behavior: smooth;
  }

  .output-line {
    margin-bottom: 8px;
    line-height: 1.4;
  }

  /* Style scrollbar */
  .output-container::-webkit-scrollbar {
    width: 8px;
  }

  .output-container::-webkit-scrollbar-track {
    background: #1e1e1e;
  }

  .output-container::-webkit-scrollbar-thumb {
    background: #4af626;
    border-radius: 4px;
  }
</style>
