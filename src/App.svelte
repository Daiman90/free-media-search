<script>
	import {openFilterModel, closeModal} from './components/Modal.svelte';
	import {checkFilter} from './components/Filter.svelte';
	import Unsplash from './components/Unsplash.svelte';
	import Pixabay from './components/Pixabay.svelte';
	import PexelsImg from './components/PexelsImg.svelte';
	import PexelsVideo from './components/PexelsVideo.svelte';
	import GIF from './components/Giphy.svelte';
	let search = '';
	let loading = false;

	  
	async function formSubmitted(event) {
		event.preventDefault();
		const lastResults = await document.querySelectorAll('.results');
		await lastResults.forEach(result => {
			result.parentNode.removeChild(result);
		})

		let unsplash = await new Unsplash({
			target: document.body,
			props: {
				search: search,
			}
		})

		let pixabay = await new Pixabay({
			target: document.body,
			props: {
				search: search,
			}
		})

		let pexelsImg = await new PexelsImg({
			target: document.body,
			props: {
				search: search,
			}
		})

		let pexelsVideo = await new PexelsVideo({
			target: document.body,
			props: {
				search: search,
			}
		})

		let gif = await new GIF({
			target: document.body,
			props: {
				search: search,
			}
		})

		loading = false;
		await checkFilter();
	};
</script>

<style>
	form {display: grid; width: 50%; margin: 0 auto;}
	.filter {font-size: 0.8rem; text-decoration: underline;}
	.submit {width: 40%; justify-self: end;}
	button:hover {cursor: pointer; background-color: grey; border-color: grey; color: white;}

	.search {color: white;}
	.model {
		z-index: -999;
		opacity: 0;
		display: grid; 
		justify-content: center; 
		align-items: center; 
		text-align: center; 
		background: rgba(0, 0, 0, 0.8); 
		position: fixed; 
		top: 0; 
		right: 0; 
		left: 0; 
		bottom: 0;
		}

		.close-btn {
			position: fixed;
			top: 2%;
			right: 2%;
		}
		
		.close-btn:hover {
			cursor: pointer;
		}

		.media-close {font-size: 2rem;}

		.model-item-filter {
			position: fixed;
			top: 35%;
			left: 50%;
			transform: translate(-50%, -50%);
			width: 70%;
			height: 30%;
			background: white;
		}

		.filter-checkbox {
			font-size: 1.3rem; 
			list-style-type: none; 
			column-count: 2; 
			text-align: start;
			margin: auto;
			position: relative;
			top: 50%;
			left: 50%;
			transform: translate(-50%, -50%);
			}

		.model-item-1 {
			position: fixed;
			top: 35%;
			left: 50%;
			transform: translate(-50%, -50%);
			width: 70%;
			height: 60%;
			background-image: url(test.jpg);
			background-position: center;
			background-size: cover;
		}

		.model-item-2 {
			position: fixed;
			bottom: 15%;
			left: 50%;
			transform: translate(-50%, -50%);
		}

		.copy-img {
			width: 200%;
			transform: translateX(-25%);
		}
</style>

{#if loading}
	<img src="https://media.giphy.com/media/4ilFRqgbzbx4c/giphy.gif" alt="loading">
{/if}

<form on:submit={formSubmitted} class="form">
	<label class="search" for="search">Search</label>
	<input bind:value={search} id="search" name="search" type="text">
	<div class="filter">
		<a href="#" on:click={openFilterModel}>Filter</a>
	</div>
	<button class="submit" type="submit">Submit</button>
</form>

<div class="media-model model">
<div on:click={closeModal} class="close-btn media-close">&#x274c;</div>
	<div class="model-item-1"></div>
	<div class="model-item-2">
		<div class="download">
			<a href="#" class="download-btn" target="_blank" download>
				<button>
					Download
				</button>
				</a>
		</div>
		<input class="copy-img" type="text" readonly value="#">
	</div>
</div>

<div class="filter-model model">
	<div class="model-item-filter">
		<div on:click={closeModal} class="close-btn filter-close">&#x274c;</div>
		<ul class="filter-checkbox">
			<li><input type="checkbox" on:change={() => this.classList.toggle('true')} on:change={checkFilter} name="filter" value="img"> Image</li>
			<li><input type="checkbox" on:change={() => this.classList.toggle('true')} on:change={checkFilter} name="filter" value="video"> Video</li>
			<li><input type="checkbox" on:change={() => this.classList.toggle('true')} on:change={checkFilter} name="filter" value="gif"> GIF</li>
			<li><input type="checkbox" on:change={() => this.classList.toggle('true')} on:change={checkFilter} name="filter" value="unsplash"> Unsplash</li>
			<li><input type="checkbox" on:change={() => this.classList.toggle('true')} on:change={checkFilter} name="filter" value="pixabay"> Pixabay</li>
			<li><input type="checkbox" on:change={() => this.classList.toggle('true')} on:change={checkFilter} name="filter" value="pexels"> Pexels</li>
			<li><input type="checkbox" on:change={() => this.classList.toggle('true')} on:change={checkFilter} name="filter" value="giphy"> Giphy</li>
		</ul>
	</div>
</div>
