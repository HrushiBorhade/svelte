<script lang="ts">
  import Image from "../components/Image.svelte";
  import CanvasContainer from "../components/Canvas.Container.svelte";

  const rickFacts = [
    "Did you know? Rick Astley's 'Never Gonna Give You Up' was released in 1987!",
    "The term <b>'Rickrolling'</b> became popular on 4chan in 2007!",
    "Rick Astley himself got <b>Rickrolled</b> on Reddit in 2020!",
    "The original video has over <b>1.2 billion</b> views on YouTube!",
    "Rick Astley was only <b>21 years old</b> when he recorded the song!",
    "Rick Astley is a <b>legend</b>!",
    "The music video was shot in <b>one day</b> at various locations in London!",
    "Rick Astley won <b>Best British Male Singer</b> at the 1988 Brit Awards!",
    "The song reached <b>#1</b> in 25 countries worldwide!",
    "Rick Astley initially <b>retired</b> from the music industry in 1993!",
    "The song's co-writer Pete Waterman called it <b>'the perfect pop record'</b>!",
  ];

  let index = $state(0);
  let fact = $derived(rickFacts[index]);
  let name = $state("Hrushi");
  $inspect(index).with(console.trace);

  $effect(() => {
    console.log(`Fact changed to: ${fact}`);
  });

  function incrementIndex() {
    index = (index + 1) % rickFacts.length;
  }

  async function getTodos() {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();
    return data;
  }
</script>

<div class="container">
  <CanvasContainer />
  <h1>YOU'VE BEEN RICKROLLED!</h1>

  <Image {index} />

  <p>{@html fact}</p>

  <button onclick={incrementIndex}>Show Another Fun Fact!</button>

  <input type="text" bind:value={name} />
  <p>Hey, {name}!</p>

  {#if index > 5}
    <p>You've seen a lot of facts!</p>
  {:else if index == 0}
    <p>Click the button to see a fun fact!</p>
  {:else}
    <p>You've seen a few facts!</p>
  {/if}

  <h1>list of facts</h1>
  <div>
    {#each rickFacts as fact, i}
      <p>{i + 1}: {@html fact}</p>
    {/each}
  </div>

  <h1>list of todos</h1>

  {#await getTodos()}
    <p>Loading...</p>
  {:then todos}
    {#each todos.slice(0, 10) as todo, i}
      <p>{i + 1}: {todo.title}</p>
    {/each}
  {:catch error}
    <p>Error: {error}</p>
  {/await}
</div>

<style>
  :global(body) {
    background-color: #1a1a1a;
    margin: 0;
    padding: 1rem;
  }

  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 1.5rem;
    max-width: 800px;
    margin: 0 auto;
  }

  h1 {
    color: #ff4444;
    font-family: "Comic Sans MS", cursive;
    font-size: 2.5em;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
    animation: bounce 1s infinite;
    z-index: -1;
  }

  @keyframes bounce {
    0%, 100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-10px);
    }
  }

  p {
    color: #e0e0e0;
    font-size: 1.2em;
    text-align: center;
    font-family: Arial, sans-serif;
    background-color: #2a2a2a;
    padding: 1rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    max-width: 600px;
  }

  input {
    background-color: #2a2a2a;
    color: #e0e0e0;
    padding: 1rem;
    border-radius: 8px;
    border: none;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    font-size: 1.2em;
    max-width: 600px;
  }

  button {
    background-color: #ff4444;
    color: white;
    font-weight: bold;
    padding: 15px 30px;
    border-radius: 8px;
    cursor: pointer;
    font-family: "Comic Sans MS", cursive;
    font-size: 1.2em;
    border: none;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
    transition: all 0.3s ease;
  }

  button:hover {
    background-color: #ff6666;
    transform: translateY(-2px);
    box-shadow: 0 6px 8px rgba(0, 0, 0, 0.3);
  }

</style>
