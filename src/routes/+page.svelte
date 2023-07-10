<script lang="ts">
	import type { PageData } from './$types';
	import type { IndexMonster } from './+page';
	import { page } from '$app/stores';
	import { generations } from './generations';
	import { goto } from '$app/navigation';

	export let data: PageData;
	$: monsterID = $page.url.searchParams.get('monsterID') || '';
	$: monster = data.monsters.find((monster) => monster.id === monsterID);
	$: monster2ID = $page.url.searchParams.get('monster2ID') || '';
	$: monster2 = data.monsters.find((monster) => monster.id === monster2ID);

	const updateSearchParams = (key: string, value: string) => {
		const searchParams = new URLSearchParams($page.url.searchParams);
		searchParams.set(key, value);
		goto(`?${searchParams.toString()}`);
	};
</script>

<h1>{monsterID}</h1>
<h3>{monster?.name}</h3>
<h1>{monster2ID}</h1>
<h3>{monster2?.name}</h3>

<div class="generations">
	{#each generations as generation (generation.id)}
		<div class="generation">
			{generation.main_region}
		</div>
	{/each}
</div>

<div class="monsters">
	{#each data.monsters as monster (monster.id)}
		<div class="monster">
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<!-- svelte-ignore a11y-no-static-element-interactions -->
			<div on:click={() => updateSearchParams('monsterID', monster.id)}>
				<div class="monster-content">
					<img src={monster.image} alt={monster.name} />
					<p>{monster.name}</p>
				</div>
				<div class="monster-id">{monster.id}</div>
			</div>
			<!-- svelte-ignore a11y-click-events-have-key-events -->
			<!-- svelte-ignore a11y-no-static-element-interactions -->
			<button class="secondary" on:click={() => updateSearchParams('monster2ID', monster.id)}>
				Add as secondary
			</button>
		</div>
	{/each}
</div>

<style>
	.generations {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
	}

	.generation {
		margin: 5px;
		padding: 5px 10px;
		border: 1px solid black;
		background-color: #f9f9f9;
		color: #333;
	}

	.generation:hover {
		background-color: #eee;
	}

	p {
		margin: 0;
	}

	.monsters {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
	}

	.monster {
		width: 100px;
		margin: 10px;
		padding: 10px;
		position: relative;
		background-color: #eee;
		cursor: pointer;
	}

	.monster:hover {
		background-color: #ddd;
	}

	.monster-content {
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.monster-id {
		position: absolute;
		top: 5px;
		left: 5px;
		font-size: 0.8em;
		font-weight: bold;
		color: #888;
	}

	.secondary {
		text-align: center;
		background-color: #ddd;
		cursor: pointer;
	}

	.secondary:hover {
		background-color: #eee;
	}
</style>
