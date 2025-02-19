<script lang="ts">
  import { RxStomp } from "@stomp/rx-stomp"
  import type { ChatMessage } from "./types"
  import { onMount } from "svelte"
  import { map } from "rxjs/operators"

  export let rxStomp: RxStomp
  export let topic: string

  let chatMessages: ChatMessage[] = [
    { userName: "admin", message: `Welcome to ${topic} room!`}
  ]

  onMount(() => {
    const messageSubscription = rxStomp
      .watch(topic)
      .pipe(map((payload) => JSON.parse(payload.body)))
      .subscribe((chatMessage) => chatMessages = [...chatMessages, chatMessage])

    return () => messageSubscription.unsubscribe()
  })
</script>

<h2>Messages</h2>
<ul>
{#each chatMessages as chatMessage}
  <li><strong>{chatMessage.userName}</strong>: {chatMessage.message}</li>
{/each}
</ul>