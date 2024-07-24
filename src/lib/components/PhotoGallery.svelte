<script>
	export let images = [];
	export let openModal = () => {
	};
</script>

<main class="grid grid-cols-3 gap-1">
	{#each images as image}
		<div
			class="hover:opacity-70 aspect-photos square-image hover:cursor-pointer"
			on:click|preventDefault={() => openModal(image)}>
			<img alt="image" class="object-fit bg-neutral-100 dark:bg-neutral-900" loading="lazy" src={image} />
		</div>
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