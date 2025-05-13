<script>
  export let args = [];

  const contacts = [
    { type: "Email", value: "hello@myportfolio.com", icon: "✉️" },
    { type: "GitHub", value: "github.com/myusername", icon: "🐙" },
    { type: "LinkedIn", value: "linkedin.com/in/myprofile", icon: "🔗" },
    { type: "Twitter", value: "@myhandle", icon: "🐦" },
  ];
</script>

<div class="command-output contact">
  <h3>Contact Me</h3>

  {#each contacts as contact}
    <div class="contact-method">
      <span class="icon">{contact.icon}</span>
      <span class="type">{contact.type}:</span>
      <span class="value">{contact.value}</span>
    </div>
  {/each}

  <p class="note">
    Feel free to reach out for collaborations or just to say hi!
  </p>
</div>

<style>
  .contact h3 {
    color: #4af626;
    margin-bottom: 15px;
  }

  .contact-method {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
  }

  .icon {
    margin-right: 10px;
    font-size: 1.2rem;
  }

  .type {
    font-weight: bold;
    margin-right: 5px;
    min-width: 70px;
  }

  .note {
    margin-top: 15px;
    font-style: italic;
    color: #aaa;
  }
</style>
