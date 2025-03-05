<script lang="ts">
    const monkeys = [
        ['🙈', 'see no evil'],
        ['🙉', 'hear no evil'],
        ['🙊', 'speak no evil']
    ];
</script>
{#snippet monkey(emoji: string, description: string)}
<tr>
	<td>{emoji}</td>
	<td>{description}</td>
	<td>\u{emoji.charCodeAt(0).toString(16)}\u{emoji.charCodeAt(1).toString(16)}</td>
	<td>&amp#{emoji.codePointAt(0)}</td>
</tr>
{/snippet}

<table>
	<thead>
		<tr>
			<th>emoji</th>
			<th>description</th>
			<th>unicode escape sequence</th>
			<th>html entity</th>
		</tr>
	</thead>

	<tbody>
        {#each monkeys as [emoji, description]}
		{@render monkey(emoji, description)}
        {/each}
	</tbody>
</table>

<style>
	table {
		padding: 1rem;
		border-radius: 1rem;
		box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.5);
		border: 1px solid #fff;
	}
	th, td {
		padding: 0.5em;
		color: #fff;
	}

	td:nth-child(3),
	td:nth-child(4) {
		font-family: monospace;
		font-size: 1.2em;
		color: #fff;
	}
</style>
