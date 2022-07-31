<script lang="ts">
  import Tile from './Tile.svelte';
  let tiles = Array(9).fill(0);
  let activePlayer:number = 1;
  function clickTileHandler(tileIndex:number){
    tiles[tileIndex] = 0;
  }

</script>

<div id="matchfield">
  {#each tiles as tile, i}
    <Tile checkedFrom={tile} on:click={clickTileHandler(i)}/>
  {/each}
</div>

<style>
#matchfield{
  aspect-ratio: 1;
  background-color: rgba(255, 255, 255, 0.87);
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(3, 1fr);
  place-items: center;
  gap: 2%;
  padding: 2%;
  border-radius: 3%;
}
</style> 
