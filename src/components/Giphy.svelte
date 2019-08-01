	<script>
		import { openMediaModal } from './Modal.svelte';

		export let search = "";
		export let GIF = [];

		(async() => {
		 	const GIF_KEY = 'mCwKOpoiOnD7gQT5fc8JKzBO1noWaw6q';
			const GIF_API_URL = `http://api.giphy.com/v1/gifs/search?limit=100&api_key=`

			const gifApi = `${GIF_API_URL}${GIF_KEY}&q=${search}`
			const gifResponse = await fetch(gifApi);

			const gifJson = await gifResponse.json();

			GIF = gifJson.data.map(gif => {
				let result = {
					"photos": gif.images.original.url,
						"urls": gif.images.original.url
				}
        return result
      });
		})();

  </script>

	<style>
		.results {column-count: 3;}
		img {width: 100%; height: auto;}
	</style>

<div class="results">
	{#each GIF as gif}
		<a on:click={openMediaModal} href={gif.urls} target="_blank" class="gif giphy single-item">
			<img src={gif.photos} alt="photo" />
		</a>
  {/each}
</div>