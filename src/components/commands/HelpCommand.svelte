<script>
  export let args = [];
</script>

<div class="command-output help">
  <h3>Available Commands:</h3>
  <table>
    <tbody>
      <tr>
        <td><span class="command">help</span></td>
        <td>Show this help message</td>
      </tr>
      <tr>
        <td><span class="command">about</span></td>
        <td>Show information about me</td>
      </tr>
      <tr>
        <td><span class="command">projects</span></td>
        <td>List my projects</td>
      </tr>
      <tr>
        <td><span class="command">contact</span></td>
        <td>Show my contact information</td>
      </tr>
      <tr>
        <td><span class="command">clear</span></td>
        <td>Clear the terminal</td>
      </tr>
    </tbody>
  </table>
</div>

<style>
  .help table {
    border-collapse: collapse;
    margin-top: 10px;
  }

  .help tr td:first-child {
    padding-right: 20px;
    color: #4af626;
  }

  .help tr td {
    padding-bottom: 8px;
    vertical-align: top;
  }

  .help h3 {
    margin-bottom: 5px;
    color: #f0f0f0;
  }
</style>
