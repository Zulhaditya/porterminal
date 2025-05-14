<script>
  export const args = [];

  const projects = [
    {
      name: "Terminal Portfolio",
      description: "This interactive portfolio website with terminal theme",
    },
    {
      name: "E-commerce Platform",
      description: "Full-featured online store with payment integration",
    },
    {
      name: "Task Management App",
      description: "Productivity application for team collaboration",
    },
    {
      name: "Task Management App",
      description: "Productivity application for team collaboration",
    },
  ];
</script>

<div class="command-output projects">
  <h3>My Projects</h3>

  {#each projects as project, i}
    <div class="project">
      <h4>{i + 1}. {project.name}</h4>
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

  .project h4 {
    color: #f0f0f0;
    margin: 0 0 5px 0;
  }

  .project p {
    color: white;
    margin: 0;
    padding: 0;
  }
</style>
