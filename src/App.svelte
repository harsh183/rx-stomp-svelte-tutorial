<script lang="ts">
  import { RxStomp, type RxStompConfig } from "@stomp/rx-stomp"
  import { onMount } from "svelte"
  import Status from "./Status.svelte"
  import Chatroom from "./Chatroom.svelte"

  const rxStomp = new RxStomp()
  onMount(() => {
    const rxStompConfig: RxStompConfig = {
      brokerURL: "ws://localhost:15674/ws",
      connectHeaders: {
        login: "guest",
        passcode: "guest",
      },
      debug: (msg) => {
        console.log(new Date(), msg)
      },
      heartbeatIncoming: 0,
      heartbeatOutgoing: 20000,
      reconnectDelay: 200,
    }

    rxStomp.configure(rxStompConfig)
    rxStomp.activate()

    return () => rxStomp.deactivate()
  })

  let inChatroom = false
  const toggleChatroom = () => inChatroom = !inChatroom
</script>

<main>
  <h1>Hello RxStomp x Svelte</h1>
  <Status {rxStomp}/>

  {#if inChatroom }
    <button on:click={toggleChatroom}>
      Leave chatroom!
    </button>

    <Chatroom {rxStomp} />
  {:else}
    <button on:click={toggleChatroom}>
      Join Chatroom
    </button>
  {/if}
</main>
