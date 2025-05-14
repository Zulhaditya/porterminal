<script>
  import CommandLine from "./CommandLine.svelte";
  import OutputDisplay from "./OutputDisplay.svelte";

  // Command components
  import Help from "./commands/Help.svelte";
  import About from "./commands/About.svelte";
  import Projects from "./commands/Projects.svelte";
  import Contact from "./commands/Contact.svelte";
  import Clear from "./commands/Clear.svelte";
  import Home from "./commands/Home.svelte";

  let commandHistory = [];
  let outputHistory = [];
  let currentArgs = null;
  let CommandComponent = null;

  // Available commands
  const commands = {
    help: Help,
    about: About,
    projects: Projects,
    contact: Contact,
    home: Home,
    clear: Clear,
  };

  function handleCommand(event) {
    const command = typeof event === "string" ? event : event.detail;
    commandHistory = [...commandHistory, command];

    // Process command and generate output
    const output = processCommand(command);
    // Add to output history
    if (output) {
      outputHistory = [...outputHistory, output];
    }
  }

  function processCommand(input) {
    try {
      // Handle undefined/null input
      if (input == null) {
        return "Error: No command provided";
      }

      // Convert to string if it's not
      const inputStr = String(input);
      const trimmedInput = inputStr.trim();

      // Handle empty input after trim
      if (trimmedInput === "") return "";

      const [command, ...args] = trimmedInput.split(" ");
      const cmd = command.toLowerCase();

      // Special case for clear command
      if (cmd === "clear") {
        outputHistory = [];
        commandHistory = [];
        CommandComponent = null;
        return "";
      }

      if (!commands[cmd]) {
        return `Command not found: ${cmd}. Type <span class="command">help</span> for available commands.`;
      }

      CommandComponent = commands[cmd];
      currentArgs = args;
      outputHistory = [];
      return "";
    } catch (error) {
      console.error("Error processing command:", error);
      return `Error: Failed to process command (${error.message})`;
    }
  }
</script>

<div class="terminal">
  <div class="terminal-header">
    <div class="terminal-buttons">
      <span class="close"></span>
      <span class="minimize"></span>
      <span class="maximize"></span>
    </div>
    <span class="terminal-title">root@debian: ~</span>
  </div>

  <div class="terminal-body">
    {#if CommandComponent && CommandComponent !== Clear}
      <svelte:component this={CommandComponent} args={currentArgs} />
    {/if}

    <OutputDisplay {outputHistory} />
    <CommandLine on:command={(e) => handleCommand(e.detail)} />
  </div>
</div>

<style>
  .terminal {
    width: 80%;
    max-width: 1280px;
    height: 550px;
    margin: 2rem auto;
    background-color: #1e1e1e;
    border-radius: 8px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
    display: flex;
    flex-direction: column;
    font-family: "Courier New", monospace;
  }

  .terminal-header {
    background-color: #333;
    padding: 8px 12px;
    display: flex;
    align-items: center;
  }

  .terminal-title {
    color: #aaa;
    font-size: 0.9rem;
  }

  .terminal-body {
    flex: 1;
    padding: 15px;
    color: #f0f0f0;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
  }

  .terminal-buttons {
    display: flex;
    gap: 8px;
    margin-right: 12px;
  }

  .terminal-buttons span {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    display: inline-block;
  }

  .close {
    background-color: #ff5f56;
  }
  .minimize {
    background-color: #ffbd2e;
  }
  .maximize {
    background-color: #27c93f;
  }
</style>
