<script>
  export let guilds;
  export let activeGuild;
  export let setActiveGuild;

  function handleGuildClick(guild) {
    setActiveGuild(guild);
  }
</script>

<div class="guilds">
  {#each Object.keys(guilds) as guild}
    <div class="guild" on:click={() => handleGuildClick(guild)}>
      {guild}
    </div>
  {/each}
  <div class="bottom-box"></div>
</div>

<style>
  .guilds {
    width: 55px;
    background: #1f2024;
    color: white;
    padding: 10px;
    position: relative;
  }
  .guild {
    cursor: pointer;
    padding: 5px;
  }
  .guild:hover {
    background: #424549;
  }
</style>
