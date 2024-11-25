<script>
  export let guilds;
  export let activeGuild;
  export let setActiveGuild;

  function handleGuildClick(guild) {
    setActiveGuild(guild);
  }
</script>

<div class="guilds">
  <div class="guild-list">
     <div style="border-bottom:1px solid #a1a1a1; border-radius:0%; " class="guild">
        <p>home</p>
     </div>
    {#each Object.keys(guilds) as guild}
      <div class="guild" on:click={() => handleGuildClick(guild)}>
        <p>{guild}</p>
      </div>
    {/each}
  </div>
  <div class="bottom-box"><button style="font-size:8px;margin:5% 25%;border-radius:50%;height:40px;width:40px;background:#424549;color:white;">discovery</button></div>
  
</div>

<style>
  p{
    font-size:10px;
  }
  .guilds {
    display: flex;
    flex-direction: column;
    width: 50px;
    background: #1f2024;
    color: white;
    height: 100vh;
  }
  .guild-list {
    flex: 1;
    overflow-y: scroll;
  }
  .guild {
    border-radius:50%; 
    height:35px;
    width:35px;
    cursor: pointer;
  }
  .guild:hover {
    background: #424549;
  }
  .bottom-box {
    height: 55px;
    width:80px;
    margin-left:-20px;
    background: #1a1a1a;
  }
</style>
