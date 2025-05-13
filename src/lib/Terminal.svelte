<script>
  import { Terminal } from "@xterm/xterm";
  import { FitAddon } from "@xterm/addon-fit";
  import { onMount } from "svelte";

  let terminalContainer;

  // list command and output
  const commands = {
    help: "\nAvailable commands: about, projects, contact, clear",
    about: "\nI am a developer who loves terminal UIs!",
    projects: "\nProject 1: Terminal Portfolio | Project 2: ...",
    contact: "\nEmail: me@example.com",
  };

  onMount(() => {
    const terminal = new Terminal({
      cursorBlink: true,
      scrollback: Infinity,
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
    terminal.writeln('Welcome chad! Type "help" to see commands.\r\n');
    terminal.write("$ ");

    // Handle input
    let currentInput = "";
    terminal.onData((data) => {
      if (data === "\r") {
        // Enter
        processCommand(terminal, currentInput);
        currentInput = "";
        terminal.scrollToBottom();
      } else if (data === "\x7f") {
        // Backspace
        if (terminal.buffer.active.cursorX > 2) {
          terminal.write("\b \b");
          currentInput = currentInput.slice(0, -1);
        }
      } else if (data >= " " && data <= "~") {
        terminal.write(data);
        currentInput += data;
        // Auto-scroll saat mengetik panjang
        if (terminal.buffer.active.cursorY >= terminal.rows - 1) {
          terminal.scrollToBottom();
        }
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
        term.writeln(`\nCommand not found: "${command}"`);
      }

      // Reset prompt
      term.write("\n$ ");
      term.scrollToBottom();
    }

    // Handle resize
    window.addEventListener("resize", () => {
      fitAddon.fit();
      terminal.scrollToBottom(); // Scroll ke bawah setelah resize
    });
  });
</script>

<div class="terminal-container">
  <div bind:this={terminalContainer} class="terminal" />
</div>

<style>
  .terminal-container {
    width: 100%;
    height: 100vh;
    padding: 1rem;
    background-color: black;
    border: 1px solid #00ff00;
    border-radius: 4px;
    box-shadow: 0 0 10px rgba(0, 255, 0, 0.3);
    overflow: hidden;
    padding: 1rem;
  }

  .terminal {
    width: 100%;
    height: 100%;
    padding: 0;
    margin: 0;
  }

  /* Scrollbar styling */
  :global(.xterm-viewport) {
    overflow-y: scroll !important;
    scrollbar-color: #00ff00 #000000;
  }

  :global(.xterm-viewport::-webkit-scrollbar) {
    width: 8px;
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
