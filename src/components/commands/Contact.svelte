<script>
  export const args = [];

  const contacts = [
    { type: "Gmail", value: "zulhaditya@gmail.com" },
    { type: "GitHub", value: "github.com/zulhaditya" },
    { type: "LinkedIn", value: "linkedin.com/in/zulhaditya" },
    { type: "Twitter", value: "x.com/ackxle" },
  ];
</script>

<div class="command-output contact">
  <h3>Contact Me</h3>

  {#each contacts as contact}
    <div class="contact-method">
      <span class="type">{contact.type}:</span>
      <a href="https://{contact.value}" target="_blank" class="value"
        >{contact.value}</a
      >
    </div>
  {/each}

  <p class="note">
    Feel free to reach out for collaborations or just to say hi!
  </p>
</div>

<style>
  .contact {
    padding-left: 2rem;
  }
  .contact h3 {
    color: white;
    font-weight: bold;
    margin-bottom: 15px;
  }

  .contact-method {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
  }

  .type {
    font-weight: bold;
    margin-right: 5px;
    min-width: 70px;
    color: #4af626;
  }

  .value {
    color: white;
  }

  .note {
    margin-top: 15px;
    color: white;
  }
</style>
