<script lang="ts">
  import Image from "../components/Image.svelte";

  const rickFacts = [
    "Did you know? Rick Astley's 'Never Gonna Give You Up' was released in 1987!",
    "The term <b>'Rickrolling'</b> became popular on 4chan in 2007!",
    "Rick Astley himself got <b>Rickrolled</b> on Reddit in 2020!",
    "The original video has over <b>1.2 billion</b> views on YouTube!",
    "Rick Astley was only <b>21 years old</b> when he recorded the song!",
  ];

  let index = $state(0);
  let fact = $derived(rickFacts[index]);

  $inspect(index).with(console.trace);

  $effect(() => {
    console.log(`Fact changed to: ${fact}`);
  });

  function incrementIndex() {
    index = (index + 1) % rickFacts.length;
  }
</script>

<div class="container">
  <h1>YOU'VE BEEN RICKROLLED!</h1>

  <Image {index} />

  <p>{@html fact}</p>

  <button onclick={incrementIndex}>Show Another Fun Fact!</button>
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

  @keyframes bounce {
    0%,
    100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-10px);
    }
  }
</style>
