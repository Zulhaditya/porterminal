<script>
  import { createEventDispatcher } from "svelte";
  import { onMount } from "svelte";

  const dispatch = createEventDispatcher();
  let command = "";
  let inputElement;

  function focusOnAnyKey(node) {
    const handleKeyDown = () => node.focus();

    document.addEventListener("keydown", handleKeyDown);

    return {
      destroy() {
        document.removeEventListener("keydown", handleKeyDown);
      },
    };
  }

  // onMount(() => {
  //   inputElement.focus();
  // });

  function handleSubmit(e) {
    e.preventDefault();
    const cmd = command.trim();
    if (cmd) {
      dispatch("command", {
        detail: cmd, // Pastikan mengirim sebagai properti detail
      });
      command = "";
    }
  }
</script>

<form on:submit={handleSubmit} class="command-line">
  <span class="prompt">$</span>
  <input
    type="text"
    use:focusOnAnyKey
    bind:value={command}
    class="command-input"
    autocomplete="off"
    autocorrect="off"
    autocapitalize="off"
    spellcheck="false"
  />
</form>

<style>
  .command-line {
    display: flex;
    align-items: center;
    margin-bottom: 1rem;
  }

  .prompt {
    color: #4af626;
    margin-right: 8px;
  }

  .command-input {
    background: transparent;
    border: none;
    color: #f0f0f0;
    font-family: "Courier New", monospace;
    font-size: 1rem;
    flex: 1;
    outline: none;
    caret-color: #4af626;
  }
</style>
