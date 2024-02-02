<script>
	import { onMount } from 'svelte';
	import toast, { Toaster } from 'svelte-french-toast';
	let formData = {
		name: '',
		age: ''
	};
	let label = '';
	let message = '';
	let submitted = false;
	function showContent() {
		submitted = true;
		if (formData.name.length == 0 || formData.age.length == 0) {
			label = 'error';
		} else {
			label = 'success';
			message = `${formData.name} is of age ${formData.age}`;
			formData.name = formData.age = '';
		}
	}

	onMount(() => {
		if (label == 'success') toast.success('Form submitted successfully');
		else toast.error('Please fill out all fields');
	});
</script>

<div class="container">
	<h1>Details</h1>
	<form>
		<label class="labels" for="name">Name:</label>
		<input
			type="text"
			bind:value={formData.name}
			name="name"
			id="name"
			placeholder="Enter your name"
		/>
		<label class="labels" for="age">Age:</label>
		<input type="text" bind:value={formData.age} name="age" id="age" placeholder="Enter your age" />
		<button type="submit" class="submitButton" on:click={showContent}>Submit</button>
	</form>
	{#if submitted}
		<Toaster />
	{/if}
</div>
{#if label == 'success'}
	<div class="container">
		<p>{message}</p>
	</div>{/if}

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
	h1 {
		text-align: center;
	}
	form {
		display: flex;
		flex-direction: column;
	}
	label {
		font-size: 18px;
		margin-bottom: 5px;
	}

	input {
		padding: 10px;
		margin-bottom: 20px;

		font-size: 16px;
		border-radius: 15px;
		border: none;
		box-shadow: 0 3px 10px rgba(22, 26, 27, 0.459);
	}
	.submitButton {
		padding: 10px;
		border: none;
		border-radius: 15px;
		color: white;
		font-size: 18px;
		background-color: #007bff;
		cursor: pointer;
		box-shadow: 0 3px 10px rgba(22, 26, 27, 0.459);
	}
	.submitButton:hover {
		background-color: #015fc4;
	}
</style>
