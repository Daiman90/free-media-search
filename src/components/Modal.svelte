<script context="module">
  export function openMediaModal(event) {
    event.preventDefault();
		const modal = document.querySelector('.model');
		const modalItem = document.querySelector('.model-item-1');
		const modalButton = document.querySelector('.download-btn');
		const copyImg = document.querySelector('.copy-img');
		
		const img = this.querySelector('img').src;
		const link = this.href;

		modal.style.zIndex = '999';
		modal.style.opacity = '1';
		modalItem.style.backgroundImage = `url(${img})`;
		modalButton.href = link;
		copyImg.value = img;
	};
	
	export function openFilterModel(event) {
		event.preventDefault();

		const modal = document.querySelector('.filter-model')
		modal.style.zIndex = '999';
		modal.style.opacity = '1';
	};

	export function closeModal() {
		const modal = document.querySelectorAll('.model');
		modal.forEach(modal => {
			modal.style.zIndex = '-999';
			modal.style.opacity = '0';

		})
	}	

</script>

