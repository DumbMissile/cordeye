<script>
  import { onMount } from 'svelte';
  import Guilds from './components/Guilds.svelte';
  import Channels from './components/Channels.svelte';
  import Chat from './components/Chat.svelte';
  import UserList from './components/UserList.svelte';

  let guilds = {
    'skibidi sigmas': {
      channels: ['General', 'Gifts', 'Coal'],
      channelMessages: {
        General: [
          { user: 'Mark', content: 'im gooning' },
          { user: 'Chud', content: 'KYS' },
        ],
        Gifts: [],
        Coal: [],
      },
    },
    'ohio': {
      channels: ['General', 'Gooning', 'meow'],
      channelMessages: {
        General: [],
        Gooning: [{user:'Mark',content:'i cant stop gooning'}],
        meow: [],
      },
    },
  };

  let activeGuild = 'skibidi sigmas';
  let activeChannel = 'General';
  let newMessage = '';
  let messages = guilds[activeGuild].channelMessages[activeChannel];
  let users = ['Chud', 'Mark', 'You']; 
  
  $: messages = guilds[activeGuild].channelMessages[activeChannel];

  function sendMessage() {
    if (newMessage.trim()) {
      guilds[activeGuild].channelMessages[activeChannel].push({ user: 'You', content: newMessage });
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
    display: flex;
    height: 100vh;
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
  <UserList {users} />
</div>
