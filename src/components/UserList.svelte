<script>
  export let users;
</script>

<div class="users">
  <h2>Users</h2>
  <ul>
    {#each users as user}
      <li>{user}</li>
    {/each}
  </ul>
</div>

<style>
  .users {
    width: 200px;
    background: #2f3136;
    color: white;
    padding: 10px;
  }
</style>
