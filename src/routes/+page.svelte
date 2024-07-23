<script>
	import Topbar from '$components/Topbar.svelte';
	import ProfileHeader from '$components/ProfileHeader.svelte';
	import Footer from '$components/Footer.svelte';
	import PhotoGallery from '$components/PhotoGallery.svelte';
	import VideoGallery from '$components/VideoGallery.svelte';
	import Modal from '$components/Modal.svelte';
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
	import { writable } from 'svelte/store';

	let contentTypeStore = writable('photo');
	let showModal = false;
	let selectedImageUrl = '';

	const images = Object.values(import.meta.glob('../../contents/images/*.{avif,gif,heif,jpeg,jpg,png,tiff,webp,svg}', {
		eager: true,
		query: '?url',
		import: 'default'
	})).sort((a, b) => a.localeCompare(b));

	const videos = [
		{
			id: 1,
			video: 'https://via.placeholder.com/150'
		}
	];

	const numberPosts = images.length + videos.length;

	onMount(() => {
		const params = new URLSearchParams(window.location.search);
		const type = params.get('type');
		contentTypeStore.set(type === 'video' ? 'video' : 'photo');

		$: document.title = `helmyl/gallery/${$contentTypeStore}s`;

		const handleKeyDown = (event) => {
			if (event.key.toLowerCase() === 'm') {
				showModal = true;
			}
			if (event.key === 'Escape') {
				showModal = false;
			}
		};

		window.addEventListener('keydown', handleKeyDown);

		return () => {
			window.removeEventListener('keydown', handleKeyDown);
		};
	});

	function updateContentType(type) {
		contentTypeStore.set(type);
		goto(`?type=${type}`, { replaceState: true });
	}

	function openModal(imageUrl) {
		selectedImageUrl = imageUrl;
		showModal = true;
		document.body.style.overflow = 'hidden';
	}

	function closeModal() {
		showModal = false;
		document.body.style.overflow = 'auto';
	}
</script>

<div class="min-h-screen bg-white dark:bg-black dark:text-neutral-200">
	<Topbar />
	<div class="flex items-center justify-between w-full my-5">
		<div class="md:w-11/12 lg:w-7/12 mx-auto">
			<ProfileHeader numberPosts={numberPosts} />
			<div class="flex items-center justify-center text-center gap-5 border-t mb-4 dark:border-neutral-800">
				<button
					class="uppercase tracking-tight font-semibold text-sm pt-3 px-3 border-black {$contentTypeStore === 'photo' ? 'border-t dark:border-neutral-400' : ''}"
					on:click={() => updateContentType('photo')}
				>
					Photos
				</button>

				<button
					class="uppercase tracking-tight font-semibold text-sm pt-3 px-3 border-black {$contentTypeStore === 'video' ? 'border-t dark:border-neutral-400' : ''}"
					on:click={() => updateContentType('video')}
				>
					Videos
				</button>
			</div>

			<Modal {closeModal} {showModal}>
				<img alt={selectedImageUrl} class="z-20 cursor-default" src={selectedImageUrl}>
			</Modal>

			{#if $contentTypeStore === 'photo'}
				{#if images.length === 0}
					<p class="text-center">No photos found</p>
				{:else}
					<PhotoGallery {images} {openModal} />
				{/if}
			{:else if $contentTypeStore === 'video'}
				{#if videos.length === 0}
					<p class="text-center">No videos found</p>
				{:else}
					<VideoGallery {videos} />
				{/if}
			{/if}
		</div>
	</div>

	<Footer />
</div>
