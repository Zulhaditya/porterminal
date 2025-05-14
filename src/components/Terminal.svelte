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
  import Neofetch from "./commands/Neofetch.svelte";

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
    neofetch: Neofetch,
    calc: {
      render: () => "",
    },
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

      // Handle calculator expressions
      if (trimmedInput.startsWith("calc ")) {
        const expression = trimmedInput.substring(5).trim();
        if (!expression) return "Usage: calc <expression>";

        try {
          const result = evaluateMathExpression(expression);
          return `= ${result}`;
        } catch (error) {
          return `Math Error: ${error.message}`;
        }
      }

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

  // Fungsi evaluasi ekspresi matematika
  function evaluateMathExpression(expr) {
    // Bersihkan input dan validasi
    const cleanExpr = expr.replace(/[^-()\d/*+.]/g, "");

    // Validasi karakter berbahaya
    if (cleanExpr !== expr.replace(/[^a-zA-Z0-9\-()\d/*+.]/g, "")) {
      throw new Error("Invalid characters in expression");
    }

    try {
      // Gunakan Function constructor sebagai alternatif eval yang lebih aman
      const result = new Function(`return ${cleanExpr}`)();

      // Handle pembagian oleh nol
      if (!isFinite(result)) {
        throw new Error("Division by zero or infinite result");
      }

      return result;
    } catch (error) {
      throw new Error(`Invalid expression: ${error.message}`);
    }
  }
</script>

<div class="aesthetic-background"></div>
<div class="terminal">
  <div class="terminal-header">
    <div class="terminal-buttons">
      <span class="close"></span>
      <span class="minimize"></span>
      <span class="maximize"></span>
    </div>
    <span class="terminal-title">kitty</span>
  </div>

  <div class="terminal-body">
    {#if CommandComponent && CommandComponent !== Clear}
      <svelte:component this={CommandComponent} args={currentArgs} />
    {/if}

    <OutputDisplay {outputHistory} {commandHistory} />
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

  .aesthetic-background {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: linear-gradient(135deg, #0f0f0f 0%, #1a1a1a 50%, #0f0f0f 100%);
    z-index: -1;
  }

  .aesthetic-background::before {
    content: "";
    top: -10rem;
    left: -10rem;
    width: calc(100% + 20rem);
    height: calc(100% + 20rem);
    z-index: 9999;
    position: fixed;
    background-image: url(https://upload.wikimedia.org/wikipedia/commons/5/5c/Image_gaussian_noise_example.png);
    opacity: 0.15;
    pointer-events: none;
    -webkit-animation: noise 1s steps(2) infinite;
    animation: noise 1s steps(2) infinite;
  }

  @-webkit-keyframes noise {
    to {
      transform: translate3d(-7rem, 0, 0);
    }
  }

  @keyframes noise {
    0% {
      transform: translate3d(0, 9rem, 0);
    }
    10% {
      transform: translate3d(-1rem, -4rem, 0);
    }
    20% {
      transform: translate3d(-8rem, 2rem, 0);
    }
    30% {
      transform: translate3d(9rem, -9rem, 0);
    }
    40% {
      transform: translate3d(-2rem, 7rem, 0);
    }
    50% {
      transform: translate3d(-9rem, -4rem, 0);
    }
    60% {
      transform: translate3d(2rem, 6rem, 0);
    }
    70% {
      transform: translate3d(7rem, -8rem, 0);
    }
    80% {
      transform: translate3d(-9rem, 1rem, 0);
    }
    90% {
      transform: translate3d(6rem, -5rem, 0);
    }
    to {
      transform: translate3d(-7rem, 0, 0);
    }
  }
</style>
