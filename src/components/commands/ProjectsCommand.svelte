<script>
  export let args = [];

  const projects = [
    {
      name: "Terminal Portfolio",
      description: "This interactive portfolio website with terminal theme",
      tech: ["Svelte", "JavaScript", "CSS"],
    },
    {
      name: "E-commerce Platform",
      description: "Full-featured online store with payment integration",
      tech: ["React", "Node.js", "MongoDB"],
    },
    {
      name: "Task Management App",
      description: "Productivity application for team collaboration",
      tech: ["Vue", "Firebase", "Vuex"],
    },
  ];
</script>

<div class="command-output projects">
  <h3>My Projects</h3>

  {#each projects as project}
    <div class="project">
      <h4>{project.name}</h4>
      <p>{project.description}</p>
      <div class="tech">
        {#each project.tech as tech}
          <span class="tech-tag">{tech}</span>
        {/each}
      </div>
    </div>
  {/each}
</div>

<style>
  .projects h3 {
    color: #4af626;
    margin-bottom: 15px;
  }

  .project {
    margin-bottom: 20px;
    padding-bottom: 15px;
    border-bottom: 1px solid #333;
  }

  .project h4 {
    color: #f0f0f0;
    margin: 0 0 5px 0;
  }

  .tech {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 8px;
  }

  .tech-tag {
    background-color: #333;
    color: #4af626;
    padding: 3px 8px;
    border-radius: 4px;
    font-size: 0.8rem;
  }
</style>
