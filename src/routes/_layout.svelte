<script>
	import Header from '../components/shared/Header.svelte';
</script>

<style>
	main {
        margin-top: 5rem;
    }
</style>

<Header />

<main>
	<slot></slot>
</main>