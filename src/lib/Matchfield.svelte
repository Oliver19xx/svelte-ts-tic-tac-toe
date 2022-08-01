<script lang="ts">
  import Tile from "./Tile.svelte";
  import PlayerMarker from "./PlayerMarker.svelte";
  let tiles = Array(9).fill(0);
  let activePlayer: number = 1;
  let winner = 0;
  let winningLine = "";
  function clickTileHandler(tileIndex: number) {
    tiles[tileIndex] = activePlayer;
    activePlayer = activePlayer === 1 ? 2 : 1;
    checkWhichPlayerFillOneRow();
  }
  function checkWhichPlayerFillOneRow(): void {
    const allEqual = (arr) => arr.every((val) => val === arr[0]);

    if (allEqual([tiles[0], tiles[1], tiles[2]]) && tiles[0] !== 0) {
      winningLine = "02";
      winner = tiles[0];
    } else if (allEqual([tiles[3], tiles[4], tiles[5]]) && tiles[3] !== 0) {
      winningLine = "35";
      winner = tiles[3];
    } else if (allEqual([tiles[6], tiles[7], tiles[8]]) && tiles[6] !== 0) {
      winningLine = "68";
      winner = tiles[6];
    } else if (allEqual([tiles[0], tiles[3], tiles[6]]) && tiles[0] !== 0) {
      winningLine = "06";
      winner = tiles[0];
    } else if (allEqual([tiles[1], tiles[4], tiles[7]]) && tiles[1] !== 0) {
      winningLine = "17";
      winner = tiles[1];
    } else if (allEqual([tiles[2], tiles[5], tiles[8]]) && tiles[2] !== 0) {
      winningLine = "28";
      winner = tiles[2];
    } else if (allEqual([tiles[0], tiles[4], tiles[8]]) && tiles[0] !== 0) {
      winningLine = "08";
      winner = tiles[0];
    } else if (allEqual([tiles[2], tiles[4], tiles[6]]) && tiles[2] !== 0) {
      winningLine = "26";
      winner = tiles[2];
    }
  }
  // TODO: Logic in Funktion auslagern, welche bei jedem Rendern aufgerufen wird.
  /*function isWinningLineVisible(label:string):boolean{
    console.log(winner,winningLine,label,winner !== 0 && winningLine === label);
    return winner !== 0 && winningLine === label;
  }*/
</script>

<div id="matchfield">
  {#each tiles as tile, i}
    <Tile checkedFrom={tile} on:click={() => clickTileHandler(i)} />
  {/each}
  {#if winner !== 0}
    <div id="interaction-blocker" />
  {/if}
  {#if winner !== 0 && winningLine !== ""}
    <div
      id="winning-line-{winningLine}"
      class="winning-line 
      {['02', '35', '68'].includes(winningLine) ? 'horizontal' : null}
      {['06', '17', '28', '08', '26'].includes(winningLine) ? 'vertical' : null}
      {winner ? 'p' + winner : null}
      "
    />
  {/if}
</div>
<div class="game-state">
  {#if winner === 0}
    <h2>Active Player:</h2>
    <div class="player-marker">
      <PlayerMarker id={activePlayer} />
    </div>
  {:else}
    <h2>Winner is Player</h2>
    <div class="player-marker">
      <PlayerMarker id={winner} />
    </div>
  {/if}
</div>

<style>
  #matchfield {
    aspect-ratio: 1;
    background-color: rgba(255, 255, 255, 0.87);
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
    place-items: center;
    gap: 2%;
    padding: 2%;
    border-radius: 3%;
    position: relative;
  }
  #interaction-blocker {
    position: absolute;
    width: 100%;
    height: 100%;
  }

  .game-state {
    display: flex;
    gap: 10px;
    place-items: center;
    place-content: center;
  }

  .game-state .player-marker {
    display: inline-block;
    max-width: 2em;
  }
  .winning-line {
    position: absolute;
    border-radius: 10px;
    box-shadow: 0px 0px 5px 0px;
    height: 3%;
    width: 3%;
  }
  .winning-line.p1 {
    background: #ffce26;
  }
  .winning-line.p2 {
    background: #4ac4ff;
  }
  .winning-line.horizontal {
    height: 3%;
    width: 94%;
    transition: width 2s;
  }
  .winning-line.vertical {
    height: 94%;
    width: 3%;
    transition: height 2s;
  }

  #winning-line-02 {
    top: 15.8%;
  }
  #winning-line-35 {
    top: 48.7%;
  }
  #winning-line-68 {
    top: 81%;
  }
  #winning-line-06 {
    left: 15.8%;
  }
  #winning-line-17 {
    left: 48.7%;
  }
  #winning-line-28 {
    left: 81%;
  }
  #winning-line-08 {
    top: -12%;
    left: 49%;
    transform-origin: center;
    transform: rotate(-45deg);
    height: 124%;
  }
  #winning-line-26 {
    top: -12%;
    left: 49%;
    transform-origin: center;
    transform: rotate(45deg);
    height: 124%;
  }
</style>
