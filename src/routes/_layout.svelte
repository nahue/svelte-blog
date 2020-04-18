<script>
	import Nav from '../components/Nav.svelte';

	export let segment;
</script>

<main class="relative bg-white overflow-hidden">
	<div class="relative pt-6 pb-16 md:pb-20">
		<Nav {segment}/>
	</div>
	<slot></slot>
</main>