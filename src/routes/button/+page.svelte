<script>
	//declaring props
	export let label;
	export let isDisabled;
	export let handleClick;
</script>

<button on:click={handleClick(label)} disabled={isDisabled}>
	{label}
</button>

<style>
	button {
		box-shadow: 0 3px 10px rgba(22, 26, 27, 0.459);
		padding: 1em;
		border-radius: 20px;
		font-family: 'Roboto';
		font-size: 16px;
		border: none;
		padding: 1em;
	}
</style>
