<script>
  import Card from "./Card.svelte";
  import { parseInput } from "./bingo.js";

  let complete = false;
  let { selectedNumbers, boards } = parseInput();

  async function playGames() {
    for (const number of selectedNumbers) {
      await new Promise(r => setTimeout(r, 300));
      boards
        .filter(board => !board.hasWon())
        .forEach(board => board.play(number));
      boards = boards;
      const winners = boards.filter(board => board.hasWon());
      if (boards.every(board => board.hasWon())) {
        complete = true;
        return;
      }
    }
  }

  async function replay() {
    complete = false;
    boards = parseInput().boards;
    await new Promise(r => setTimeout(r, 1500));
    playGames();
  }

  playGames();
</script>

<style>
  :global(body) {
    background-color: #ddbea9;
    margin: 16px;
  }

  :global(*) {
    box-sizing: border-box;
  }

  main {
    font-family: sans-serif;
    text-align: center;
  }

  .grid {
    display: inline-grid;
    grid-template-columns: repeat(10, auto);
    gap: 8px;
    margin: 16px;
    background: url(/squid.svg) center no-repeat;
    background-size: contain;
  }

  a,
  a:visited {
    color: #cb997e;
  }
</style>

<main>
  <div class="grid">
    {#each boards as board}
      <Card {board} />	
    {/each}
  </div>
  
  <footer>
    <a href="https://github.com/aoneill01/bingo">repository</a><br />
    {#if complete}
      <a href={'#'} on:click={replay}>replay</a>
    {/if}
  </footer>
</main>