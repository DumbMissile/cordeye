<script>
  import { onMount } from 'svelte';
  import Guilds from './components/Guilds.svelte';
  import Channels from './components/Channels.svelte';
  import Chat from './components/Chat.svelte';
  import UserList from './components/UserList.svelte';
  import data from './guilds.json';
  
  let guilds = data.guilds;
  let activeGuild = 'skibidi sigmas';
  let activeChannel = 'General';
  let newMessage = '';
  let messages = guilds[activeGuild].channelMessages[activeChannel];
  let users = guilds[activeGuild].users;
  $: messages = guilds[activeGuild].channelMessages[activeChannel];

  function sendMessage() {
    if (newMessage.trim()) {
      guilds[activeGuild].channelMessages[activeChannel].push({ user: guilds[activeGuild].users[0], content: newMessage });
      messages=guilds[activeGuild].channelMessages[activeChannel]
      newMessage = ''; 
      scrollToBottom();
    }
  }
 
  function handleKeyPress(event) {
    if (event.key === 'Enter') {
      event.preventDefault();
      sendMessage();
    }
  }

  function scrollToBottom() {
    const messagesContainer = document.querySelector('.messages');
    if (messagesContainer) {
      setTimeout(() => {
        messagesContainer.scrollTop = messagesContainer.scrollHeight;
      }, 0);
    }
  }

  function setActiveGuild(guild) {
    activeGuild = guild;
    activeChannel = guilds[guild].channels[0];
  }

  function setActiveChannel(channel) {
    activeChannel = channel;
  }

  onMount(() => {
    scrollToBottom();
  });
</script>

<style>
  :global(body) {
    background: #1f2024;
  }

  .container {
    margin-top:-5px;
    display: flex;
    height: 80vw;
  }
</style>



<div class="container">
  <Guilds {guilds} {activeGuild} setActiveGuild={setActiveGuild} />
  <Channels 
    activeGuild={activeGuild} 
    channels={guilds[activeGuild].channels} 
    activeChannel={activeChannel} 
    setActiveChannel={setActiveChannel} 
  />
  <Chat 
    {messages} 
    activeChannel={activeChannel}
    bind:newMessage 
    sendMessage={sendMessage} 
    handleKeyPress={handleKeyPress} 
  />
  <UserList users={guilds[activeGuild].users} />
</div>

