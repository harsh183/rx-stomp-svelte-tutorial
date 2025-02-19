<script lang="ts">
  import { RxStompState, type RxStomp } from "@stomp/rx-stomp"
  import { onMount } from "svelte"

  let connectionStatus = ''

  export let rxStomp: RxStomp

  onMount(() => {
    const statusSubscription = rxStomp.connectionState$.subscribe((state) => { 
      connectionStatus = RxStompState[state]
    })

    return () => statusSubscription.unsubscribe()
  })
</script>

<h2>Connection Status: {connectionStatus}</h2>