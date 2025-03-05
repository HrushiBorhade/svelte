<script lang="ts">
	import { count } from './shared';
</script>

<button on:click={() => count.update((n) => n + 1)}>Click me</button>
<p>Count: {$count}</p>


<style>

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
</style>
