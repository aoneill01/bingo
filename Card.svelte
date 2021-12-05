<script>
  export let board;

  $: complete = board.hasWon();
</script>

<style>
  .card {
    background-color: #6b705c;
    width: 75px;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    padding: 5px;
    gap: 2px;
    transition: opacity 0.6s ease-in-out 1s;
    font-size: 8px;
    font-weight: bold;
    color: #a5a58d;
  }
  .cell {
    background-color: #ffe8d6;
    aspect-ratio: 1;
    transition: background-color 0.4s ease-in-out;
  }

  .cell.win {
    background-color: #cb997e;
  }

  .selected {
    background-color: #b7b7a4;
  }

  .complete {
    opacity: 0.25;
  }
</style>

<div class="card" class:complete={complete}>
  <div>B</div>
  <div>I</div>
  <div>N</div>
  <div>G</div>
  <div>O</div>
  {#each board.selectedSquares as row, r}
    {#each row as selected, c}
      <div class="cell" class:win={board.isWinningSquare(r, c)} class:selected={selected}>&nbsp;</div>
    {/each}
  {/each}
</div>