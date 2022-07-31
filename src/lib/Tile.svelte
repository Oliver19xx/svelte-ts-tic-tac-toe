<script lang="ts">
  import PlayerMarker from './PlayerMarker.svelte';
  export let checkedFrom:number = 0;
</script>

<button class="tile" on:click>
  {#if checkedFrom !== 0}
    <PlayerMarker id={checkedFrom}/>
  {:else}
  <div></div>
  {/if}
</button>

<style>
.tile{
  display: flex;
  place-items: center;
  width: -webkit-fill-available;
  aspect-ratio: 1;
  background-color:#242424;
  border-radius: 8%;
  max-height: 100px;
  overflow: hidden
}

button{
  padding:0;
}
.tile > div {
    display: flex;
}
</style>