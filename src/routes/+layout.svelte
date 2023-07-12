<script lang="ts">
	import { page } from '$app/stores';
</script>

<div class="navbar">
	<a href="/" class:active={$page.url.pathname == '/'}>Home</a>
	<a href="/my-monsters" class:active={$page.url.pathname == '/my-monsters'}>My Monsters</a>
</div>

<div class="container">
	<slot />
</div>

<style>
	.navbar {
		display: flex;
		justify-content: space-between;
		padding: 10px 30px;
		background-color: #333;
		color: #fff;
		position: sticky;
		top: 0;
		left: 0;
		z-index: 1;
	}

	.navbar a {
		text-decoration: none;
		color: #fff;
		padding: 5px;
	}

	.navbar a:hover {
		color: #ccc;
	}

	.navbar a.active {
		color: #ccc;
		border: #ccc solid 1px;
		border-radius: 4px;
	}

	:global(body) {
		margin: 0;
		padding: 0;
		font-family: 'Didact Gothic', sans-serif;
	}

	:global(button) {
		font-family: 'Didact Gothic', sans-serif;
	}

	.container {
		width: 1200px;
		max-width: 90%;
		margin: 0 auto;
	}
</style>
