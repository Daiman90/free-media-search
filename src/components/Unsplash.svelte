	<script>
		import { openMediaModal } from './Modal.svelte';
		// import { UNSPLASH_ACCESS_KEY } from '../keys.svelte';
		export let search = "";
		export let unsplashPhotos = [];

		(async() => {
			unsplashPhotos = [];
			const UNSPLASHKEY = 'e65a58390fd87054d56e6d19d040180fed627edb0971a07a8ccbaf21a3561818';
			const UNSPLASH_API_URL = `https://api.unsplash.com/search/photos?page=1&per_page=100&client_id=`
	
			const unsplashApi = `${UNSPLASH_API_URL}${UNSPLASHKEY}&query=${search}`
			const unsplashResponse = await fetch(unsplashApi);
	
			const unsplashJson = await unsplashResponse.json();
	
			 unsplashPhotos = unsplashJson.results.map(photo => {
				 let result = {
					 "photos": photo.urls.regular,
						 "urls": photo.links.download
				 }
				 return result
			 })
			
		})();

  </script>

	<style>
		.results {column-count: 3;}
		img {width: 100%; height: auto;}
	</style>

<div class="results">
	{#each unsplashPhotos as photo}
		<a on:click={openMediaModal} href={photo.urls} target="_blank" class="img unsplash single-item">
			<img src={photo.photos} alt="photo" />
		</a>
	{/each}
</div>