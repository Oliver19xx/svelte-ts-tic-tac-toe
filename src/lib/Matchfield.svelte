<script lang="ts">
  import Tile from './Tile.svelte';
  import PlayerMarker from './PlayerMarker.svelte';
  let tiles = Array(9).fill(0);
  let activePlayer:number = 1;
  let winner = 0;
  let winningLine = '';
  let isGameFinished:boolean = false;
  function clickTileHandler(tileIndex:number){
    tiles[tileIndex] = activePlayer;
    activePlayer = activePlayer === 1? 2:1;
    checkIfGameFinished();
  };
  function checkIfGameFinished():void{
    checkWhichPlayerFillOneRow();
    isGameFinished = winner !==0 || tiles.filter(tile => tile ===0).length === 0;
  }
  function checkWhichPlayerFillOneRow():void{
    const allEqual = arr => arr.every(val => val === arr[0]);

    if(allEqual(tiles[0],tiles[1],tiles[2]) && tiles[0]!== 0){
      winningLine='02';
      winner = tiles[0];
    }
    else if(allEqual(tiles[3],tiles[4],tiles[5]) && tiles[3]!== 0){
      winningLine='35';
      winner = tiles[3];
    }
    else if(allEqual(tiles[6],tiles[7],tiles[8]) && tiles[6]!== 0){
      winningLine='68';
      winner = tiles[6];
    }
    else if(allEqual(tiles[0],tiles[3],tiles[6]) && tiles[0]!== 0){
      winningLine='06';
      winner = tiles[0];
    }
    else if(allEqual(tiles[1],tiles[4],tiles[7]) && tiles[1]!== 0){
      winningLine='17';
      winner = tiles[1];
    }
    else if(allEqual(tiles[2],tiles[5],tiles[8]) && tiles[2]!== 0){
      winningLine='28';
      winner = tiles[2];
    }
    else if(allEqual(tiles[0],tiles[4],tiles[8]) && tiles[0]!== 0){
      winningLine='08';
      winner = tiles[0];
    }
    else if(allEqual(tiles[2],tiles[4],tiles[6]) && tiles[2]!== 0){
      winningLine='26';
      winner = tiles[2];
    }
  }
</script>

<div id="matchfield">
  {#each tiles as tile, i}
    <Tile checkedFrom={tile} on:click={()=>clickTileHandler(i)}/>
  {/each}
</div>
<div class="game-state">
  {#if !isGameFinished}
  <h2>
    Active Player: 
  </h2>
  <div class="player-marker">
    <PlayerMarker id={activePlayer} />
  </div>
  {:else}
  <h2>
    Winner is Player
  </h2>
  <div class="player-marker">
    <PlayerMarker id={winner} />
  </div>
  {/if}
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

.game-state{
  display: flex;
  gap: 10px;
  place-items: center;
  place-content:center;
}

.game-state .player-marker{
  display: inline-block;
  max-width: 2em;
}
</style> 
