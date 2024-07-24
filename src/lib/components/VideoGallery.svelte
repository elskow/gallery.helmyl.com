<script>
	export let videos = [];
</script>

<main class="grid grid-cols-3 gap-1">
	{#each videos as { video }}
		<button on:click={() => window.open(video, '_blank')} class="hover:opacity-70 aspect-photos square-image">
			<img alt="video" class="bg-neutral-100 dark:bg-neutral-900"
					 width="540" height="540" src={video} />
		</button>
	{/each}
</main>

<style>
    .square-image {
        width: 100%;
        height: 0;
        padding-top: 100%;
        position: relative;
    }

    .square-image img {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
    }
</style>