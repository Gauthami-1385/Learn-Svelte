<script>
	import toast, { Toaster } from 'svelte-french-toast';

	let value;
	let lang = ['C', 'C++', 'Java', 'Python3', 'Javascript'];
	function handleSelect(e) {
		toast.success(`You have selected ${e.target.value}!`, {
			style: 'border: 1px solid #26A65B; padding: 16px; color: #26A65B;',
			iconTheme: {
				primary: '#26A65B',
				secondary: '#fff'
			}
		});
	}
</script>

<div class="container">
	<label for="language">Choose your Programming:</label>
	<select name="language" on:change={handleSelect}>
		<option value="" selected disabled>Select an option</option>
		{#each lang as language}
			<option value={language}>{language}</option>
		{/each}
	</select>

	<Toaster />
</div>

<style>
	.container {
		background-color: white;
		margin: 50px auto;
		max-width: 500px;
		padding: 3em;
		box-shadow: 0 3px 10px rgba(22, 26, 27, 0.459);
		border-radius: 15px;
		font-family: sans-serif;
	}
	option {
		/* height: 30px; */
		border-radius: 5px;
		background-color: white;
		font-size: 16px;
		font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
	}
</style>
