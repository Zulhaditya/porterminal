<script>
  import { Terminal } from "@xterm/xterm";
  import { FitAddon } from "@xterm/addon-fit";
  import { onMount } from "svelte";

  let terminalContainer;

  // list command and output
  const commands = {
    help: "Available commands: about, projects, contact, clear",
    about: "I am a developer who loves terminal UIs!",
    projects: "Project 1: Terminal Portfolio | Project 2: ...",
    contact: "Email: me@example.com",
  };

  onMount(() => {
    const terminal = new Terminal({
      cursorBlink: true,
      fontFamily: '"Courier New", monospace',
      fontSize: 16,
      theme: {
        background: "#000000",
        foreground: "#00ff00",
        cursor: "#00ff00",
      },
      rows: 30,
      screenReaderMode: false,
    });

    const fitAddon = new FitAddon();
    terminal.loadAddon(fitAddon);
    terminal.open(terminalContainer);
    fitAddon.fit();

    // Prompt awal
    terminal.writeln(
      'Welcome to my terminal portfolio! Type "help" to see commands.\r\n',
    );
    terminal.write("$ ");

    // Handle input
    let currentInput = "";
    terminal.onData((data) => {
      if (data === "\r") {
        // Enter
        processCommand(terminal, currentInput);
        currentInput = "";
      } else if (data === "\x7f") {
        // Backspace
        if (terminal.buffer.active.cursorX > 2) {
          terminal.write("\b \b");
          currentInput = currentInput.slice(0, -1);
        }
      } else if (data >= " " && data <= "~") {
        terminal.write(data);
        currentInput += data;
      }
    });

    function processCommand(term, input) {
      const command = input.trim().split(" ")[0];
      term.writeln("");

      if (commands[command]) {
        term.writeln(commands[command]);
      } else if (command === "clear") {
        term.clear();
      } else if (command) {
        term.writeln(`Command not found: "${command}"`);
      }

      // Reset prompt
      term.write("\n$ ");
    }

    // Handle resize
    window.addEventListener("resize", () => fitAddon.fit());
  });
</script>

<div bind:this={terminalContainer} class="terminal" />

<style>
  .terminal {
    width: 100%;
    height: 70vh;
    padding: 1rem;
    background-color: black;
    border: 1px solid #00ff00;
    border-radius: 4px;
    box-shadow: 0 0 10px rgba(0, 255, 0, 0.3);
    overflow: hidden;
    padding: 1rem;
  }

  :global(.xterm-screen .xterm-helper-textarea) {
    opacity: 0;
    /* display: none; */
  }

  :global(.xterm-screen .xterm-width-cache-measure-container) {
    opacity: 0;
    /* display: none; */
  }
</style>
