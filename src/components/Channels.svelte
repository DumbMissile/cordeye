<script>
  export let activeGuild;
  export let channels;
  export let activeChannel;
  export let setActiveChannel;
</script>

<div class="channels">
  <h4>{activeGuild}</h4>
  {#each channels as channel}
    <div class="channel" on:click={() => setActiveChannel(channel)}>
      #{channel}
    </div>
  {/each}
  <div class="bottom-box"></div>
</div>

<style>
  .channels {
    color:white;
    background: #2f3136;
    width: 200px;
  }
  .channel {
    color:white;
    cursor: pointer;
    padding: 5px;
  }
  .channel:hover {
    background: #424549;
  }
</style>
