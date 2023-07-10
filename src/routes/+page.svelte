<script lang="ts">
	import Monster from './Monster.svelte';
	import type { PageData } from './$types';
	import { page } from '$app/stores';
	import { goto } from '$app/navigation';
	import { generations } from './generations';

	export let data: PageData;

	let form = {
		searchString: ''
	};

	let searchTerm = '';

	$: selectedMonsters = data.monsters.filter((monster) => {
		return monster.name.toLowerCase().includes(searchTerm.toLowerCase());
	});

	$: monsterID = $page.url.searchParams.get('monsterID') || '';
	$: monster = data.monsters.find((monster) => monster.id === monsterID);
	$: monster2ID = $page.url.searchParams.get('monster2ID') || '';
	$: monster2 = data.monsters.find((monster) => monster.id === monster2ID);

	const updateSearchParams = (key: string, value: string) => {
		const searchParams = new URLSearchParams($page.url.searchParams);
		searchParams.set(key, value);
		goto(`?${searchParams.toString()}`);
	};

	const submitSearch = (e: Event) => {
		e.preventDefault();
		searchTerm = form.searchString;
	};
</script>

{#if monster}
	<Monster {monster} {updateSearchParams} isInteractive={false} />
{/if}

{#if monster2}
	<Monster monster={monster2} {updateSearchParams} isInteractive={false} />
{/if}

<div class="generations">
	{#each generations as generation (generation.id)}
		<div class="generation">
			{generation.main_region}
		</div>
	{/each}
</div>

<form class="search-form" on:submit={submitSearch}>
	<input type="text" bind:value={form.searchString} placeholder="Pokemon Name" />
	<input type="submit" value="Search" />
</form>

<div class="monsters">
	{#each selectedMonsters as monster (monster.id)}
		<Monster {monster} {updateSearchParams} isInteractive={true} />
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

	.monsters {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
	}

	.search-form {
		display: flex;
		justify-content: center;
		margin: 20px 0px;
	}

	.search-form input[type='text'] {
		padding: 5px 10px;
		border: 1px solid #333;
		border-radius: 5px;
		width: 200px;
	}

	.search-form input[type='submit'] {
		padding: 5px 10px;
		border: 1px solid #333;
		border-radius: 5px;
		margin-left: 10px;
		background-color: #333;
		color: #fff;
		cursor: pointer;
	}

	.search-form input[type='submit']:hover {
		background-color: #555;
	}
</style>
