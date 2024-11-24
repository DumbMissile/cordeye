
<script>
  export let users;
</script>

<div class="users">

<div class="top-box"></div>
  <h5>Users</h5>
  <ul>
    {#each users as user}
      <li class="user-item">
        <img src={user.profilePicture} class="profile-picture" />
        <span style="font-size:12px;margin-top:-10px;" class="user-name">{user.nickname || user.username}</span>
      </li>
    {/each}
  </ul>
</div>

<style>
  .users {
    width: 120px;
    background: #2f3136;
    color: white;
    border-radius: 5px;
    height:100vh;
  }
  .user-item {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
    margin-left:-30px;
    margin-top:-10px;

  }
  .profile-picture {
    width: 30px;
    height: 30px;
    border-radius: 50%; 
    margin-right: 10px;
  }
  .user-name {
    font-weight: bold;
  }
  .top-box {
    height: 30px;
    

    background: #36393f;
    border-bottom: 0.8px solid #252525;
  }
</style>
