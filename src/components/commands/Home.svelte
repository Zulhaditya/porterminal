<script>
  import { onMount } from "svelte";

  let typingComplete = false;
  let welcomeMessage = "";

  const fullMessage = `
Last login: ${new Date()}

Debian GNU/Linux 12 (bookworm) x86_64, Kernel: 6.1.0-34-amd64
  `;

  onMount(() => {
    typeWriter();
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
  </pre>

  <div class="welcome-message">
    {#if !typingComplete}
      <pre>{welcomeMessage}█</pre>
    {:else}
      <pre>{welcomeMessage}</pre>
    {/if}
  </div>
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
    line-height: 1.5;
    margin-top: 2rem;
  }

  .welcome-message {
    white-space: pre-wrap;
    text-align: center;
  }
</style>
