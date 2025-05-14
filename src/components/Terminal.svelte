<script>
  import CommandLine from "./CommandLine.svelte";
  import OutputDisplay from "./OutputDisplay.svelte";
  // Command components
  import HelpCommand from "./commands/HelpCommand.svelte";
  import AboutCommand from "./commands/AboutCommand.svelte";
  import ProjectsCommand from "./commands/ProjectsCommand.svelte";
  import ContactCommand from "./commands/ContactCommand.svelte";
  import ClearCommand from "./commands/ClearCommand.svelte";

  let commandHistory = [];
  let outputHistory = [];

  let currentArgs = null;
  let CommandComponent = null;

  // Available commands
  const commands = {
    help: HelpCommand,
    about: AboutCommand,
    projects: ProjectsCommand,
    contact: ContactCommand,
    clear: ClearCommand,
  };

  function handleCommand(event) {
    const command = typeof event === "string" ? event : event.detail;
    console.log("Command received:", command, typeof command); // Debug di sini
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

  {#if CommandComponent && CommandComponent !== ClearCommand}
    <svelte:component this={CommandComponent} args={currentArgs} />
  {/if}
  <div class="terminal-body">
    <OutputDisplay {outputHistory} />
    <CommandLine on:command={(e) => handleCommand(e.detail)} />
  </div>
</div>

<style>
  .terminal {
    width: 80%;
    max-width: 1280px;
    height: 500px;
    margin: 3rem auto;
    background-color: #1e1e1e;
    border-radius: 8px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
    overflow: hidden;
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
</style>
