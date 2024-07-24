<script lang="ts">
	import '../app.css';
	import '@fontsource-variable/public-sans';
</script>

<slot />

<style>
    :global(body) {
        font-family: 'Public Sans', sans-serif;
    }
</style>