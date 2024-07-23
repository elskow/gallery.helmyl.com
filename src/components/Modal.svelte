<script>
	import { onMount } from 'svelte';
	import { fade } from 'svelte/transition';

	export let showModal = false;
	export let closeModal;

	let modalContent, firstFocusableElement, lastFocusableElement;

	onMount(() => {
		const handleKeyDown = (event) => {
			if (event.key === 'Escape') {
				closeModal();
			} else if (event.key === 'Tab') {
				if (event.shiftKey) {
					if (document.activeElement === firstFocusableElement) {
						lastFocusableElement.focus();
						event.preventDefault();
					}
				} else {
					if (document.activeElement === lastFocusableElement) {
						firstFocusableElement.focus();
						event.preventDefault();
					}
				}
			}
		};

		window.addEventListener('keydown', handleKeyDown);

		return () => {
			window.removeEventListener('keydown', handleKeyDown);
		};
	});

	const stopPropagation = (event) => {
		event.stopPropagation();
	};
</script>

{#if showModal}
	<div class="bg-neutral-800/95 fixed w-full h-full left-0 top-0 z-30 modal-backdrop"
			 transition:fade={{ duration: 300 }} role="dialog" aria-modal="true">
		<div class="flex justify-center items-center h-full w-full" on:click={closeModal}>
			<div tabindex="-1" bind:this={modalContent} class="modal-content" aria-labelledby="modalTitle"
					 on:click={stopPropagation} transition:fade={{ duration: 300 }}>
				<button class="close-button" on:click={closeModal} aria-label="Close">&#10005;</button>
				<slot />
			</div>
		</div>
	</div>
{/if}

<style>
    .modal-content {
        min-height: 200px;
        max-width: 80%;
    }

    .close-button {
        position: absolute;
        top: 20px;
        right: 20px;
        background: transparent;
        border: none;
        color: white;
        font-size: 24px;
        cursor: pointer;
        transition: color 0.3s ease;
    }

    .close-button:hover {
        color: red;
    }

    @media (max-width: 600px) {
        .modal-content {
            max-width: 100%;
            min-height: 100px;
        }
    }
</style>