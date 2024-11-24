
<script>
  import { onMount } from 'svelte';
  export let messages;
  export let newMessage;
  export let sendMessage;

  function handleKeyPress(event) {
    if (event.key === 'Enter') {
      event.preventDefault();
      sendMessage();
    } 
  }

  function scrollToBottom() {
    const messagesContainer = document.querySelector('.messages');
    if (messagesContainer) {
      messagesContainer.scrollTop = messagesContainer.scrollHeight;
    }
  }

  onMount(() => {
    scrollToBottom();
  });
</script>

<div class="chat">
  <h2>Chat</h2>
  <div class="messages">
    {#each messages as { user, content }}
      <div class="message"><strong>{user}</strong><br> {content}</div><br>
    {/each}
  </div>
  <div class="input-container">
    <input 
      type="text" 
      bind:value={newMessage} 
      placeholder="Type a message..." 
      on:keypress={handleKeyPress} 
    />
  </div>
</div>

<style>
  .chat {
    flex: 1;
    background: #36393f;
    color: white;
    display: flex;
    flex-direction: column;
  }
  .messages {
    flex: 1;
    overflow-y: auto;
    padding: 10px;
  }
  .input-container {
    height: 60px;
    display: flex;
    margin-top: auto;
    padding: 10px;
    background: #2f3136;
  }
  input[type="text"] {
    flex: 1;
    padding: 10px;
    border: none;
    color: white;
    background-color: #424549;
    border-radius: 5px;
    margin-right: 5px;
  }
</style>
