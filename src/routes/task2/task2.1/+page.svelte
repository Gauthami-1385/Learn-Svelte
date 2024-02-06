<script>
	import toast, { Toaster } from 'svelte-french-toast';
	let formData = {
		name: '',
		password: ''
	};
	let label = '';
	let message = '';
	let submitted = false;
	let isPasswordValid = false;
	function validatePassword() {
		const passwordRegex = /^(?=.*[A-Z])(?=.*[!@#$%^&*])(?=.*[0-9]).{8,}$/;
		isPasswordValid = passwordRegex.test(formData.password);
	}

	function showContent() {
		submitted = true;
		if (formData.name.length == 0 || formData.password.length == 0) {
			label = 'error';
		} else {
			label = 'success';
			message = `${formData.name} has Logged In`;
			formData.name = formData.password = '';
		}
		if (label == 'success') toast.success('Form submitted successfully');
		else toast.error('Please fill out all fields');
	}
</script>

<div class="container">
	<h1>Details</h1>
	<form>
		<label class="labels" for="name">Username:</label>
		<input
			type="text"
			bind:value={formData.name}
			name="name"
			id="name"
			placeholder="Enter your username"
		/>
		<label class="labels" for="password">Password:</label>
		<input
			type="text"
			bind:value={formData.password}
			on:input={validatePassword}
			name="password"
			id="password"
			placeholder="Enter your password"
		/>
		<p style="color: {isPasswordValid ? 'green' : 'red'}">
			{isPasswordValid || formData.password.length == 0
				? ''
				: '*Password must have minimum length of 8 characters, one uppercase letter, one special character, least one number'}
		</p>
		<button
			type="submit"
			class="submitButton"
			on:click={showContent}
			disabled={formData.password.length == 0 || formData.name.length == 0}
			>Submit
		</button>
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
		box-shadow: 0 3px 10px rgba(25, 109, 213, 0.727);
		border-radius: 15px;
		font-family: sans-serif;
	}
	h1 {
		text-align: center;
		color: rgb(17, 63, 131);
	}
	form {
		display: flex;
		flex-direction: column;
	}
	label {
		font-size: 18px;
		margin-bottom: 5px;
		color: rgb(17, 63, 131);
	}

	input {
		padding: 10px;
		margin-bottom: 15px;
		font-size: 16px;
		border-radius: 15px;
		border: none;
		box-shadow: 0 3px 10px rgba(25, 109, 213, 0.727);
	}
	input::placeholder {
		color: rgba(17, 63, 131, 0.8);
	}
	.submitButton {
		padding: 10px;
		border: none;
		border-radius: 15px;
		color: white;
		font-size: 18px;
		background-color: rgb(17, 63, 131);
		cursor: pointer;
		box-shadow: 0 3px 10px rgba(25, 109, 213, 0.727);
	}
	.submitButton:hover {
		background-color: #015fc4;
	}
	.submitButton:disabled {
		background-color: #6a7682;
	}
</style>
