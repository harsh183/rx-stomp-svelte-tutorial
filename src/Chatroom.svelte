<script lang="ts">
  import { RxStomp } from "@stomp/rx-stomp"
  import type { ChatMessage } from "./types"
  import Messages from "./Messages.svelte";

  export let rxStomp: RxStomp

  let message = ''
  let userName = `user${Math.floor(Math.random() * 1000)}`

  const CHATROOM_NAME = '/topic/test'
  
  function sendMessage(chatMessage: ChatMessage) {
    const body = JSON.stringify(chatMessage)
    rxStomp.publish({ destination: CHATROOM_NAME, body })
    console.log(`Sent ${body}`)
    message = ''
  }
</script>

<h2>Chatroom</h2>

<label for="username">Username:</label>
<input type="text" bind:value={userName} />

<label for="message">Message:</label>
<input type="text" bind:value={message} />

<button on:click={() => sendMessage({ userName, message })}>Send Message</button>

<Messages {rxStomp} topic={CHATROOM_NAME} />