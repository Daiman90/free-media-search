<script>
	import { openMediaModal } from './Modal.svelte';

  export let search = "";
  export let pexelsPhotos = [];

  (async() => {
		pexelsPhotos = [];
		const PEXELSKEY = '563492ad6f917000010000010576ed4c98a2422bb00f5da927c7262b';
		const PEXELS_API_URL = `https://api.pexels.com/v1/search?per_page=60&page=1&query=`

			const pexelsApi = {
				url: `${PEXELS_API_URL}${search}`,
				headers: {
					'Authorization': PEXELSKEY
				}
			}

		const pexelsResponse = await fetch(`${PEXELS_API_URL}${search}`, {
			headers: {
				'Authorization': PEXELSKEY
			} 
		});

		const pexelsJson = await pexelsResponse.json();

		pexelsPhotos = pexelsJson.photos.map(photo => {
			let result = {
				"photos": photo.src.large,
				"urls": photo.src.original
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
	{#each pexelsPhotos as photo}
		<a on:click={openMediaModal} href={photo.urls} target="_blank" class="video pexels single-item">
			<img src={photo.photos} alt="photo" />
		</a>
	{/each}
</div>