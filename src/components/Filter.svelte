<script context="module">
	export function checkFilter() {
		const filteredItems = document.querySelectorAll('.true')
		let eachItem = document.querySelectorAll('.single-item');
		if(filteredItems.length !== 0) {
			eachItem.forEach(item => {
				item.style.display = 'none';
			});
			filteredItems.forEach(filtered => {
				let value = filtered.value;
				eachItem.forEach(item => {
					if(item.classList.contains(value)) {
						item.style.display = 'block';
					}
				})
			})
		}
	}
</script>
