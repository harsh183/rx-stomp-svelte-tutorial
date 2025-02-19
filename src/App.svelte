<script lang="ts">
  import { RxStomp, RxStompConfig } from "@stomp/rx-stomp"
  import { onMount } from "svelte"

  const rxStomp = new RxStomp()
</script>

<main>
  <h1>Hello RxStomp x Svelte</h1>
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
