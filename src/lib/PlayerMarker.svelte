<script lang="ts">
  import IoIosCloseCircleOutline from "svelte-icons/io/IoIosCloseCircleOutline.svelte";
  import IoIosCheckmarkCircleOutline from "svelte-icons/io/IoIosCheckmarkCircleOutline.svelte";
  export let id = 1;
</script>

<div class="player-marker {id !== 0 ? 'p' + id : null}">
  {#if id === 1}
    <IoIosCloseCircleOutline />
  {:else if id === 2}
    <IoIosCheckmarkCircleOutline />
  {/if}
</div>

<style>
  .player-marker {
    display: flex;
  }
  .p1 {
    color: #ffce26;
  }
  .p2 {
    color: #4ac4ff;
  }
</style>
