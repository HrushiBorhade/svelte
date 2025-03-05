<script lang="ts">
	import { SvelteDate } from "svelte/reactivity";
	import Counter from '../components/Counter.svelte';

	const MAX_SIZE = 200;

	class Box {
		#width = $state(0);
		#height = $state(0);
		area = $derived(this.#width * this.#height);

		constructor(width: number, height: number) {
			this.#width = width;
			this.#height = height;
		}

		get width() {
			return this.#width;
		}

		get height() {
			return this.#height;
		}

		set width(value: number) {
			this.#width = Math.max(0, Math.min(value, MAX_SIZE));
		}

		set height(value: number) {
			this.#height = Math.max(0, Math.min(value, MAX_SIZE));
		}

		embiggen(amount: number) {
			this.width += amount;
			this.height += amount;
		}
	}

	const box = new Box(100, 100);

    let date = new SvelteDate();

const pad = (n: number) => n < 10 ? '0' + n : n;

$effect(() => {
    const interval = setInterval(() => {
        date.setTime(Date.now());
    }, 1000);

    return () => {
        clearInterval(interval);
    };
});
</script>
<p>The time is {date.getHours()}:{pad(date.getMinutes())}:{pad(date.getSeconds())}</p>

<Counter />
<Counter />
<Counter />

<h1>Box</h1>

<label>
	<input type="range" bind:value={box.width} min={0} max={MAX_SIZE} />
	<p>{box.width}</p>
</label>

<label>
	<input type="range" bind:value={box.height} min={0} max={MAX_SIZE} />
	<p>{box.height}</p>
</label>

<button onclick={() => box.embiggen(10)}>embiggen</button>

<hr />

<div class="box" style:width="{box.width}px" style:height="{box.height}px">
	{box.area}
</div>

<style>
	:global(body) {
		background-color: #1a1a1a;
		margin: 0;
		padding: 1rem;
	}
	h1 {
		color: #ff4444;
		font-family: 'Comic Sans MS', cursive;
		font-size: 2.5em;
		text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
		animation: bounce 1s infinite;
		z-index: -1;
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
		font-family: 'Comic Sans MS', cursive;
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

	label {
		display: flex;
		align-items: center;
	}

	hr {
		margin: 1em 0;
		border: none;
		border-bottom: 1px solid #888;
	}

	.box {
		background: radial-gradient(at 25% 25%, hsl(15 100 60), hsl(15 100 50));
		border-radius: 2px;
		filter: drop-shadow(0 0 10px hsl(15 100 50 / 0.3));
		display: flex;
		align-items: center;
		justify-content: center;
		overflow: hidden;
	}
</style>
