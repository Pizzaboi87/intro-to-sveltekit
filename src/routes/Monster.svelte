<script lang="ts">
	import type { IndexMonster } from './+page';

	export let monster: IndexMonster;
	export let updateSearchParams: (key: string, value: string) => void;
	export let isInteractive: boolean = false;
</script>

<div class="monster" style={`${isInteractive ? 'cursor: pointer' : 'cursor: normal'}`}>
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<!-- svelte-ignore a11y-no-static-element-interactions -->
	<div on:click={() => (isInteractive ? updateSearchParams('monsterID', monster.id) : null)}>
		<div class="monster-content">
			<img src={monster.image} alt={monster.name} />
			{#if !isInteractive}
				<div class="monster-name">
					<p>{monster.name}</p>
				</div>
			{/if}
		</div>
		<div class="monster-id">{monster.id}</div>
	</div>
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<!-- svelte-ignore a11y-no-static-element-interactions -->
	{#if isInteractive}
		<div class="monster-name">
			<p>{monster.name}</p>
			<button class="secondary" on:click={() => updateSearchParams('monster2ID', monster.id)}>
				Add as secondary
			</button>
		</div>
	{/if}
</div>

<style>
	.monster {
		width: 150px;
		margin: 10px;
		padding: 10px;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: center;
		position: relative;
		background-color: #eee;
	}

	.monster:hover {
		background-color: #ddd;
	}

	.monster-content {
		display: flex;
		flex-direction: column;
	}

	.monster-id {
		position: absolute;
		top: 5px;
		left: 5px;
		font-size: 0.8em;
		font-weight: bold;
		color: #888;
	}

	.monster-name {
		display: flex;
		flex-direction: column;
		align-items: center;
		text-align: center;
		gap: 5px;
	}

	.secondary {
		text-align: center;
		background-color: #ddd;
		cursor: pointer;
	}

	.secondary:hover {
		background-color: #eee;
	}

	p {
		margin: 0;
	}
</style>
