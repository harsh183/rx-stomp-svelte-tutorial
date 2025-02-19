<script lang="ts">
  import { RxStomp, RxStompConfig } from "@stomp/rx-stomp"
  import { onMount } from "svelte"
    import Status from "./Status.svelte"

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

    return () => {
      rxStomp.deactivate()
    }
  })
</script>

<main>
  <h1>Hello RxStomp x Svelte</h1>
  <Status {rxStomp}/>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
