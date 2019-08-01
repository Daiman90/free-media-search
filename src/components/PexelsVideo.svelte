<script>
	import { openMediaModal } from './Modal.svelte';
	import { checkFilter } from './Filter.svelte';
  export let search = "";
  export let pexelsVideo = [];

  (async() => {
		pexelsVideo = [];

		const PEXELSKEY = '563492ad6f917000010000010576ed4c98a2422bb00f5da927c7262b';
		const PEXELS_VIDEO_API_URL = `https://api.pexels.com/videos/search?per_page=60&page=1&query=`

			const pexelsVideoApi = {
				url: `${PEXELS_VIDEO_API_URL}${search}`,
				headers: {
					'Authorization': PEXELSKEY
				}
			}

		const pexelsVideoResponse = await fetch(`${PEXELS_VIDEO_API_URL}${search}`, {
			headers: {
				'Authorization': PEXELSKEY
			} 
		});

		const pexelsVideoJson = await pexelsVideoResponse.json();

		pexelsVideo = pexelsVideoJson.videos.map(video => {
			let result = {
				"photos": video.image,
				"urls": video.video_files[0].link
			}
			return result
			});
			await checkFilter();
  })();

</script>

<style>
  .results {column-count: 3;}
  img {width: 100%; height: auto;}
</style>

<div class="results">
	{#each pexelsVideo as video}
		<a on:click={openMediaModal} href={video.urls} target="_blank" class="video pexels single-item">
			<img src={video.photos} alt="photo" />
		</a>
	{/each}
</div>
