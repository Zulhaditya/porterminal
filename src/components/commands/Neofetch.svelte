<script>
  let isWindows = false;

  // Detect platform (simplified)
  if (typeof window !== "undefined") {
    isWindows = navigator.platform.indexOf("Win") > -1;
  }

  // System information
  const systemInfo = {
    os: "Debian GNU/Linux 12 (bookworm) x86_64",
    host: "VivoBook_ASUSLaptop X412DK 1.0",
    kernel: "6.1.0-34-amd64",
    uptime: "2 hours, 15 mins",
    packages: "1907 (dpkg)",
    shell: "zsh 5.9",
    resolution: `${window.screen.width}x${window.screen.height}`,
    DE: "Cinnamon 5.6.8",
    WM: "Mutter (Muffin)",
    WMTheme: "cinnamon (Default)",
    Theme: "Adwaita [GTK2/3]",
    Icons: "gnome [GTK2/3]",
    terminal: "kitty",
    cpu: "AMD Ryzen 5 3500U @ 2.100GHz",
    gpu: "AMD ATI Radeon Vega Series",
    memory: "2426MiB / 15678MiB",
  };

  // ASCII Art - Choose based on OS
  const asciiArt = [
    "        _,met$$$$$gg.          ",
    "      ,g$$$$$$$$$$$$$$$P.      ",
    '    ,g$$P""       """Y$$.".    ',
    "   ,$$P'              `$$$.     ",
    " ',$$P       ,ggs.     `$$b:    ",
    " `d$$'     ,$P\"'   .    $$$     ",
    "  $$P      d$'     ,    $$P     ",
    "  $$:      $$.   -    ,d$$'     ",
    "  $$;      Y$b._   _,d$P'       ",
    '  Y$$.    `.`"Y$$$$P"\'         ',
    '  `$$b      "-.__               ',
    "   `Y$$b                        ",
    "    `Y$$.                       ",
    "      `$$b.                     ",
    "        `Y$$b.                  ",
    '          `"Y$b._               ',
    '              `""""             ',
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

  @media (max-width: 600px) {
    .neofetch-content {
      flex-direction: column;
    }

    .ascii-art {
      margin: 0 auto;
    }
  }
</style>
