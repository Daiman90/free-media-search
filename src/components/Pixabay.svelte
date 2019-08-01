<script>
	import { openMediaModal } from './Modal.svelte';
	import { checkFilter } from './Filter.svelte';
  export let search = "";
  export let pixabayPhotos = [];

  (async() => {
    pixabayPhotos = [];
    const PIXABAYKEY = '13157248-1945ca0d88bccfaee24fc3fdd'
    const PIXABAY_API_URL = `https://pixabay.com/api/?page=1&per_page=100&key=`

    const pixabayApi = `${PIXABAY_API_URL}${PIXABAYKEY}&q=${search}`
    const pixabayResponse = await fetch(pixabayApi);

    const pixabayJson = await pixabayResponse.json();

    pixabayPhotos = pixabayJson.hits.map(photo => {
      let result = {
        "photos": photo.largeImageURL,
          "urls": photo.largeImageURL
      }
      return result
    })
    await checkFilter();
  })();

</script>

<style>
  .results {column-count: 3;}
  img {width: 100%; height: auto;}
</style>

<div class="results">
	{#each pixabayPhotos as photo}
		<a on:click={openMediaModal} href={photo.urls} target="_blank" class="img unsplash single-item">
			<img src={photo.photos} alt="photo" />
		</a>
	{/each}
</div>