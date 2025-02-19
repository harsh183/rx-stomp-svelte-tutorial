<script lang="ts">
  import type { RxStomp } from "@stomp/rx-stomp"

  export let rxStomp: RxStomp
  let message = ''
  let userName = `user${Math.floor(Math.random() * 1000)}`
</script>

<h2>Chatroom</h2>

<label for="username">Username:</label>
<input type="text" bind:value={userName} />

<label for="message">Message:</label>
<input type="text" bind:value={message} />