<script>
  import { onMount } from "svelte";

  export let onContinue;
  let typingComplete = false;
  let welcomeMessage = "";

  const fullMessage = `
Last login: ${new Date()}
Type 'help' for information
  `;

  onMount(() => {
    typeWriter();
    const handleKeyDown = (e) => {
      if (e.key === "Enter" && typingComplete) {
        onContinue();
      }
    };

    window.addEventListener("keydown", handleKeyDown);
    return () => window.removeEventListener("keydown", handleKeyDown);
  });

  function typeWriter() {
    let i = 0;
    const speed = 30;

    function typing() {
      if (i < fullMessage.length) {
        welcomeMessage += fullMessage.charAt(i);
        i++;
        setTimeout(typing, speed);
      } else {
        typingComplete = true;
      }
    }

    typing();
  }
</script>

<div class="home-screen">
  <pre class="ascii-art">
⣿⣿⣿⣿⣿⣿⣿⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠿⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⢟⣵⢿⢛⣿⣿⣿⣿⣿⣿⣯⣞⣿⣿⣿⣤⣀⠀⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣽⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⢟⣽
⣿⣿⣿⣿⣯⢵⣪⣷⣿⣿⣿⣿⣿⣟⣵⢯⣿⣿⣳⣻⣿⣯⡆⢻⣿⡽⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣯⣻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⢿⣹⢾⣿⣿
⣟⢿⣻⣯⣷⣿⣿⣿⣿⡿⣿⣿⣟⣾⢏⣿⣿⢧⡏⣿⣿⣼⣿⣄⡙⠿⣮⣟⡿⠿⣿⣟⣿⣿⣿⣿⣿⣿⣿⣯⣻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣮⣵⣙⢿
⣿⣷⣿⣽⣟⣻⣿⡿⣫⣾⣿⡿⣾⠋⣼⢿⠃⣼⢹⣿⠋⣿⣿⣿⣿⣷⣶⣶⣿⢿⣶⣶⣞⣿⣿⣿⣿⣿⣿⣿⣷⡙⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⣹⣿
⣿⣿⣿⣿⣿⣿⢯⣾⣿⡿⠿⢷⠁⠀⣿⠇⠀⠁⢸⠃⠀⣿⣿⣿⣿⣿⢹⣿⣿⡏⢿⣿⣿⣞⠻⣿⢿⣿⡟⢿⣿⣷⠀⠉⠻⣿⣿⣿⣿⣿⣟⡿⣿⣷⢿
⣿⣿⣿⣿⣿⣏⡿⠋⠁⠀⠀⠀⠀⠀⡏⠀⠀⠀⠈⠀⠀⢿⡇⢻⣿⠹⡌⢻⣿⣷⠀⠋⠻⢿⠀⠈⠂⠙⢿⠀⠈⢿⡇⠀⠀⠘⠏⠻⣿⣿⣿⣟⣷⣽⡛
⣿⣿⣿⣿⣿⠉⠀⣀⣤⠂⠀⠀⠀⠀⠀⠀⢀⠀⠀⠀⠀⠸⠀⠈⢿⠀⠁⠀⠹⣿⡆⠀⠀⠀⠀⠀⠀⠀⠀⠃⠀⠀⠁⠀⠀⠀⠀⠀⠈⢯⢛⡿⣯⡻⣿
⣿⣿⣿⣿⣟⣴⣾⣿⠃⣠⡴⠀⠀⠀⠀⢰⣸⡎⠀⠀⠀⠀⠀⠀⠈⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⡀⠀⠀⠀⠀⢈⢟⣿⣷⣶⣾
⣿⣿⣿⣿⣿⣿⣿⣇⣴⣿⠇⠀⠀⠀⠀⠸⣿⣿⡄⠀⠀⠀⠀⠀⠀⠀⢀⠀⢀⣀⠀⠀⠀⠀⠀⢀⣀⠀⠀⠀⠀⠀⠀⢸⣾⡄⠀⠀⠀⢸⣮⢹⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⣿⠏⢀⣠⣤⣾⠀⢀⣿⣿⡻⢶⣦⣮⣧⡀⠘⣦⡘⡟⣨⡄⠀⠀⠀⠀⢠⣿⣏⣦⡆⠀⢠⠀⠀⢈⣿⡇⠀⠀⠀⢸⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⣷⣿⣿⣿⣿⣿⡄⣿⣿⣿⢿⣶⣶⣿⢟⣿⣖⣿⣷⣿⣿⣻⠶⣤⣤⣶⠟⣿⣿⢿⡇⢰⠏⠀⠀⠸⠋⠀⢀⠀⠀⠈⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⢿⡏⣼⣿⣷⡀⣿⣿⣿⣿⣿⣿⣿⣻⠀⠀⠀⢠⣪⡽⣿⣿⠧⠿⡶⠞⠃⠀⠀⡀⢸⣿⣶⣶⣾⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣯⡲⣿⣿⣿⣿⣾⣿⣿⣿⣿⣿⣿⣿⢄⠀⣰⣵⣦⣆⠟⠁⠀⠀⠀⠀⢠⡎⣸⡇⣼⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣮⡻⣿⣿⣿⣟⣻⢿⣿⣿⣿⣷⣾⢸⣿⠏⠞⠁⠀⠀⠠⡞⣴⣰⣿⣵⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣷⠙⢿⣦⣉⣿⣿⣿⣿⡿⠏⠚⠉⠀⠀⠀⠀⠀⢠⣾⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡁⠀⠀⠙⠿⠛⠋⠉⠀⠀⠀⠀⠀⠀⠀⠀⠀⢰⣻⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⢟⣯⣶⣦⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⣹⣷⡹⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡿⣽⣿⣿⣿⣿⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⠀⢀⣼⣿⢿⣿⣾⣝⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿
⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡗⣿⣿⢸⣿⡏⣹⣿⠀⠀⣠⣾⣿⡿⣻⣿⣿⣟⡽⠀⢰⣡⢁⣿⣿⣿⣽⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿
  </pre>

  <div class="welcome-message">
    {#if !typingComplete}
      <pre>{welcomeMessage}█</pre>
    {:else}
      <pre>{welcomeMessage}</pre>
    {/if}
  </div>

  <button class="continue-btn" on:click={onContinue} disabled={!typingComplete}>
    Press Enter to Continue
  </button>
</div>

<style>
  .home-screen {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
    color: #b5bd68;
    font-family: "Courier New", monospace;
  }

  .ascii-art {
    color: #8abeb7;
    line-height: 1;
    margin-top: 2rem;
  }

  .welcome-message {
    white-space: pre-wrap;
  }

  .continue-btn {
    background: transparent;
    border: 1px solid #4af626;
    color: #4af626;
    padding: 0.5rem 1rem;
    font-family: "Courier New", monospace;
    cursor: pointer;
    transition: all 0.3s;
  }

  .continue-btn:hover {
    background: rgba(74, 246, 38, 0.1);
  }

  .continue-btn:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
</style>
