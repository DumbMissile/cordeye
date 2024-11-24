<script>
  export let activeGuild;
  export let channels;
  export let activeChannel;
  export let setActiveChannel;
</script>

<div class="channels">
  <div class="top-box"></div>
  <h4 style="margin-left:15%;margin-top:-25px;">{activeGuild}</h4>
  <div class="channel-list">
    {#each channels as channel}
      <div class="channel" on:click={() => setActiveChannel(channel)}>
        #{channel}
      </div>
    {/each}
  </div>
  <div class="bottom-box"></div>
</div>

<style>
  .channels {
    display: flex;
    flex-direction: column;
    color: white;
    background: #2f3136;
    width: 250px;
    height: 100vh;
  }
  .channel-list {
    flex: 1;
    overflow-y: auto;
  }
  .channel {
    margin-left: 5%;
    color: white;
    cursor: pointer;
    padding: 5px;
  }
  .channel:hover {
    background: #424549;
  }
  .bottom-box {
    height: 50px;
    background: #1f2024;
  }

  .top-box {
    height: 30px;
    border-bottom: 1px solid #252525;
  }
</style>
