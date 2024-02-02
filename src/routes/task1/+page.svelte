<script>
	import Button from '../button/+page.svelte';

	let buttonLabel = [
		{ label: 'Button 1', working: false },
		{ label: 'Button 2', working: true },
		{ label: 'Button 3', working: false }
	];
	let message = '';
	const handleClick = (value) => {
		message = value + ' has been Clicked';
	};
</script>

<div class="main-container">
	<div class="container">
		{#each buttonLabel as b}
			<Button label={b.label} isDisabled={b.working} {handleClick}></Button>
		{/each}
	</div>
	<p>{message}</p>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
	.main-container {
		background-color: rgb(74, 144, 172);
		height: 100vh;
	}
	.container {
		display: flex;
		justify-content: space-around;
		align-items: center;
		padding: 5em;
	}

	p {
		text-align: center;
		color: white;
		font-weight: 700;
		font-size: large;
	}
</style>
