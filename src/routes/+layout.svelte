<script>
	import Header from './Header.svelte';
	import './styles.css';
</script>

<div class="app">
	<Header />

	<main>
		<slot />
	</main>

	<footer>
		<div>
			<p>NASA Images and Video Library <a href='https://images.nasa.gov' target='_blank' noopener noreferrer>API</a> v1.22.0</p>
			<small>© NASA 2023-01-06</small>
		</div>
	</footer>
</div>

<style>
	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		max-width: 64rem;
		margin: 0 auto;
		box-sizing: border-box;
	}

	footer {
		background-color: black;
		color: white;
	}

	footer div{
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		margin: 2rem 0;
	}

	@media (min-width: 480px) {
		footer {
			padding: 12px 0;
		}
	}
</style>
