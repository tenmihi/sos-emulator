<script lang="ts">
  import MatchGUID from "./MatchGUID.svelte";
  import WebSocket from "./WebSocket.svelte";
  import Welcome from "./Welcome.svelte";

	import { slideSideOut, slideSideIn } from "../../lib/modules/Transitions";
  import type SOS from "../../lib/SOS";

  export let sos: SOS;

  $: state = "welcome";
</script>

<firstlaunch>
  {#if state == "welcome"}
    <div class=transition out:slideSideOut>
      <Welcome bind:state={state} />
    </div>
  {:else if state == "websocket"}
    <div class=transition in:slideSideIn out:slideSideOut>
      <WebSocket bind:state={state} {sos} />
    </div>
  {:else}
    <div class=transition in:slideSideIn>
      <MatchGUID {sos} />
    </div>
  {/if}
</firstlaunch>

<style lang="scss">
  :global(body){
    overflow: hidden;
  }

  .transition {
    position: absolute;
    top: 0px;
    left: 0px;

    width: 100%;
    height: 100%;
  }
</style>