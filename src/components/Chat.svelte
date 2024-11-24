<script>
  import { onMount } from 'svelte';
  export let messages;
  export let newMessage;
  export let sendMessage;
  export let activeChannel;

  function handleKeyPress(event) {
    if (event.key === 'Enter') {
      event.preventDefault();
      sendMessage();
      scrollToBottom();
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
  <div class="top-box"></div>
  <h4 style="margin-left:2%;margin-top:-25px;">#{activeChannel}</h4>
  <div class="messages">
    {#each messages as { user, content }}
      <div class="message">
        <img src={user.profilePicture || 'default-profile.png'} class="profile-picture" />
        <div class="message-content">
          <strong>{user.nickname || user.username}</strong>
          <p>{content}</p>
        </div>
      </div>
    {/each}
  </div>
  <div class="input-container">
    <input 
      type="text" 
      bind:value={newMessage} 
      placeholder="Type a message..." 
      on:keypress={handleKeyPress} 
      aria-label="Message input"
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
    max-height:100vh;
    width: 100%;
  }
  .messages {
    flex: 1;
    overflow: auto;
    padding: 10px;
    max-width: 100%;
  }
  .message {
    display: flex;
    align-items: flex-start;
    margin-bottom: 10px;
  }
  .profile-picture {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    margin-right: 10px;
  }
  .message-content {
    background: #424549;
    border-radius: 20px;
    padding: 10px;
    max-width: 80%; 
    position: relative;
    word-wrap: break-word;
    overflow-wrap: break-word;
    white-space: normal;
    word-break: break-all;
  }
  .message-content strong {
    display: block;
    color: #7289da; 
  }
  .message-content p {
    margin: 0;
    color: #dcddde; 
  }
  .input-container {
    height: 50px;
    margin-bottom:10px;
    display: flex;
    margin-top: auto;
    padding: 10px;
  }
  input[type="text"] {
    flex: 1;
    padding: 10px;
    border: none;
    color: white;
    background-color: #404147;
    border-radius: 5px;
    margin-right: 5px;
  }
  .top-box {
    height: 30px;
    border-bottom: 1px solid #252525;
  }
</style>
