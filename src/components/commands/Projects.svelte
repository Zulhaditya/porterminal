<script>
  export const args = [];

  const projects = [
    {
      name: "Virtual Mouse",
      description:
        "Virtual mouse using webcam by implementing Hand Gesture Recognition with OpenCV.",
      link: "https://github.com/Zulhaditya/virtual-mouse",
    },
    {
      name: "Terminal Portfolio",
      description:
        "This interactive portfolio website with terminal theme using Svelte.",
      link: "https://github.com/Zulhaditya/porterminal",
    },
    {
      name: "Neopym",
      description:
        "Fast and Lightweight Neovim Configuration for your development.",
      link: "https://github.com/Zulhaditya/neopym",
    },
    {
      name: "Afiocca Website",
      description:
        "3D Portfolio Website with Admin Dashboard using Next.js and MongoDB.",
      link: "https://www.antoniofiocca.com",
    },
    {
      name: "Cyberpixel Game",
      description:
        "Action shooting game made using unity and applying the concept of the C# programming language.",
      link: "https://github.com/Zulhaditya/cyberpixels-game",
    },
  ];
</script>

<div class="command-output projects">
  <h3>My Projects</h3>

  {#each projects as project}
    <div class="project">
      <a class="title" href={project.link} target="_blank">➤ {project.name}</a>
      <p>{project.description}</p>
    </div>
  {/each}
</div>

<style>
  .projects h3 {
    color: #4af626;
    margin-bottom: 15px;
    padding-left: 2rem;
  }

  .project {
    margin-bottom: 10px;
    padding-bottom: 15px;
    padding-left: 2rem;
  }

  .project .title {
    color: #f0f0f0;
    margin: 0 0 10px 0;
    padding-bottom: 5px;
    text-decoration: none;
    font-weight: bold;
  }

  .project p {
    color: white;
    margin: 0;
    padding: 0;
  }
</style>
