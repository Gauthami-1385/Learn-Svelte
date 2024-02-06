<script>
	// let click
	let clicked = false;
	let images = [];
	let allImages = [];
	let current, selected;
	const promise = data();

	async function data() {
		const d = await fetch('https://picsum.photos/v2/list');
		const list = await d.json();
		allImages = [...list];
		images = [...allImages.slice(10, 25)];
		current = images[0].id;
	}
</script>

<div class="grid">
	{#await promise}
		<h1>loading...</h1>
	{:then _}
		<!-- {console.log(images)} -->
		{#each images as img, i}
			<div class="grid-item">
				<div class="image-container">
					<img
						class="image"
						loading="lazy"
						on:click={() => {
							clicked = true;
							current = i;
						}}
						src={img.download_url}
						alt="images"
					/>
				</div>
			</div>
		{/each}
	{/await}
</div>

{#if clicked}
	<div class="modal">
		<div
			class="close"
			on:click={() => {
				clicked = false;
			}}
		>
			x
		</div>
		<div class="modal-image">
			<div
				class="move backward"
				on:click={() => {
					if (current == 0) return;
					current -= 1;
				}}
			>
				&lt
			</div>
			<img class="m-image" loading="lazy" src={images[current]?.download_url} alt="images" />
			<div
				class="move foreward"
				on:click={() => {
					if (current == images.length - 1) current = -1;
					current += 1;
				}}
			>
				&gt
			</div>
		</div>
	</div>
{/if}

<style>
	h1 {
		text-align: center;
	}
	.grid {
		display: grid;
		border-radius: 10px;
		box-shadow:
			0 4px 8px 0 rgba(0, 0, 0, 0.2),
			0 6px 20px 0 rgba(0, 0, 0, 0.19);
		grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
		grid-gap: 0.7rem;
		margin: 50px;
		padding: 15px;
	}
	img:before {
		background: black;
	}
	.m-image {
		width: 100%;
		height: auto;
		max-height: 500px;
		object-fit: scale-down;
	}
	.close {
		cursor: pointer;
		font-size: 3rem;
		position: absolute;
		right: 0;
		color: white;
		margin-right: 1.5rem;
		top: 0;
	}
	.image {
		box-shadow:
			0 4px 8px 0 rgba(0, 0, 0, 0.2),
			0 6px 20px 0 rgba(0, 0, 0, 0.19);
		border-radius: 12px;
		cursor: pointer;
		width: 100%;
		max-width: 400px;
		max-height: 400px;
		transition: 0.125s;
	}

	.image:hover {
		opacity: 0.7;
	}

	img:active {
		opacity: 0.5;
	}
	.modal {
		position: fixed;
		z-index: 2;
		padding-top: 100px;
		left: 10%;
		top: 10%;
		width: 80%;
		border-radius: 20px;
		height: 60%;
		overflow: auto;
		background-color: rgb(0, 0, 0);
		background-color: rgba(0, 0, 0, 0.9);
	}

	.modal-image {
		margin: auto;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: center;
		flex-direction: row-reverse;
		width: 80%;
		max-width: 100%;
	}
	.move {
		position: absolute;
		z-index: 3;
		font-size: 150px;
		color: rgb(83, 79, 79);
		font-family: 'Courier New', Courier, monospace;
	}
	.backward {
		cursor: pointer;
		left: 2%;
	}
	.foreward {
		cursor: pointer;
		right: 3%;
	}
	@media screen and (max-width: 550px) {
		.modal {
			height: 35%;
		}
		.move {
			font-size: 2.5em;
			color: white;
		}

		.close {
			font-size: 3rem;
			right: 0;
			margin-right: 1.5rem;
			top: 0;
			font-size: 2em;
		}
	}
</style>
