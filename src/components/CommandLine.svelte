<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();
  let command = "";

  function focusOnAnyKey(node) {
    const handleKeyDown = () => node.focus();

    document.addEventListener("keydown", handleKeyDown);

    return {
      destroy() {
        document.removeEventListener("keydown", handleKeyDown);
      },
    };
  }

  function handleSubmit(e) {
    e.preventDefault();
    const cmd = command.trim();
    if (cmd) {
      dispatch("command", {
        detail: cmd,
      });
      command = "";
    }
  }
</script>

<form on:submit={handleSubmit} class="command-line">
  <span class="prompt">guest@debian:$</span>
  <input
    type="text"
    use:focusOnAnyKey
    bind:value={command}
    class="command-input"
    autocomplete="off"
    autocorrect="off"
    autocapitalize="off"
    spellcheck="false"
    placeholder="Type 'help' for see commands"
  />
</form>

<style>
  .command-line {
    display: flex;
    align-items: center;
    margin-bottom: 1rem;
  }

  .prompt {
    color: #8abeb7;
    margin-right: 8px;
  }

  .command-input {
    background: transparent;
    border: none;
    color: #cdcdcd;
    font-size: 1rem;
    flex: 1;
    outline: none;
    caret-color: #8abeb7;
    font-family: "Fira Code", monospace;
  }
</style>
