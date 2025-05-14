<script>
  let isWindows = false;

  // Detect platform (simplified)
  if (typeof window !== "undefined") {
    isWindows = navigator.platform.indexOf("Win") > -1;
  }

  // System information
  const systemInfo = {
    os: isWindows ? "Windows" : "Linux/WSL",
    host: "CyberSec-PC",
    kernel: isWindows ? "10.0.19045" : "5.15.90.1-microsoft-standard-WSL2",
    uptime: "2 hours, 15 mins",
    packages: isWindows ? "N/A" : "384 (pacman)",
    shell: isWindows ? "PowerShell 7.3.6" : "zsh 5.9",
    resolution: `${window.screen.width}x${window.screen.height}`,
    terminal: "Windows Terminal",
    cpu: "AMD Ryzen 7 5800X (16) @ 3.800GHz",
    gpu: "NVIDIA GeForce RTX 3060 Ti",
    memory: "16GB / 32GB",
  };

  // ASCII Art - Choose based on OS
  const asciiArt = isWindows
    ? [
        "  .+oooooooooooooooooooooooooooo+. ",
        " -oooooooooooooooooooooooooooooooo- ",
        "+oooo+///////+oooooooo+///////+oooo+",
        "oooo-         -oooooo-         -oooo",
        "oooo-         -oooooo-         -oooo",
        "+oooo+///////+oooooooo+///////+oooo+",
        " -oooooooooooooooooooooooooooooooo- ",
        "  .+oooooooooooooooooooooooooooo+. ",
      ]
    : [
        "       .-/+oossssoo+/-.       ",
        "     `:+ssssssssssssssss+:`     ",
        "   -+ssssssssssssssssssssss+-   ",
        " .osssssssssssssssssssssssssso. ",
        "+ssssssssssssssssssssssssssssss+",
        "ossyyyyyyyyyyyyyyyyyyyyyyyyyyyysso",
        "/yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy/",
        "`/yyyyyyyyyyyyyyyyyyyyyyyyyyyyyy/`",
        "  ./yyyyyyyyyyyyyyyyyyyyyyyyyy/.  ",
        "    .:oyyyyyyyyyyyyyyyyyyyo:.    ",
        "       `-/+ssyyyyysss+/-`       ",
      ];
</script>

<div class="neofetch-container">
  <div class="neofetch-content">
    <div class="ascii-art">
      {#each asciiArt as line}
        {line}<br />
      {/each}
    </div>

    <div class="info-section">
      <div>
        <span class="info-label">OS</span><span class="info-value"
          >: {systemInfo.os}</span
        >
      </div>
      <div>
        <span class="info-label">Host</span><span class="info-value"
          >: {systemInfo.host}</span
        >
      </div>
      <div>
        <span class="info-label">Kernel</span><span class="info-value"
          >: {systemInfo.kernel}</span
        >
      </div>
      <div>
        <span class="info-label">Uptime</span><span class="info-value"
          >: {systemInfo.uptime}</span
        >
      </div>
      <div>
        <span class="info-label">Packages</span><span class="info-value"
          >: {systemInfo.packages}</span
        >
      </div>
      <div>
        <span class="info-label">Shell</span><span class="info-value"
          >: {systemInfo.shell}</span
        >
      </div>
      <div>
        <span class="info-label">Resolution</span><span class="info-value"
          >: {systemInfo.resolution}</span
        >
      </div>
      <div>
        <span class="info-label">Terminal</span><span class="info-value"
          >: {systemInfo.terminal}</span
        >
      </div>
      <div>
        <span class="info-label">CPU</span><span class="info-value"
          >: {systemInfo.cpu}</span
        >
      </div>
      <div>
        <span class="info-label">GPU</span><span class="info-value"
          >: {systemInfo.gpu}</span
        >
      </div>
      <div>
        <span class="info-label">Memory</span><span class="info-value"
          >: {systemInfo.memory}</span
        >
      </div>
    </div>
  </div>
</div>

<style>
  .neofetch-container {
    color: #e0e0e0;
    padding: 3rem;
    max-width: 800px;
    margin: 0 auto;
    line-height: 1.3;
  }

  .neofetch-content {
    display: flex;
    gap: 2rem;
  }

  .ascii-art {
    color: #5e81ac;
    white-space: pre;
    font-weight: bold;
  }

  .info-label {
    color: #88c0d0;
    min-width: 100px;
    display: inline-block;
  }

  .info-value {
    color: #e5e9f0;
  }

  .title {
    color: #5e81ac;
    font-weight: bold;
    margin-bottom: 1rem;
    text-align: center;
  }

  @media (max-width: 600px) {
    .neofetch-content {
      flex-direction: column;
    }

    .ascii-art {
      margin: 0 auto;
    }
  }
</style>
