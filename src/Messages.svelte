<script lang="ts">
  import { RxStomp } from "@stomp/rx-stomp"
  import type { ChatMessage } from "./types"

  export let rxStomp: RxStomp
  export let topic: string

  let chatMessages: ChatMessage[] = [
    { userName: "admin", message: `Welcome to ${topic} room!`}
  ]
</script>

<h2>Messages</h2>
<ul>
{#each chatMessages as chatMessage}
  <li><strong>{chatMessage.userName}</strong>: {chatMessage.message}</li>
{/each}
</ul>