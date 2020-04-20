<script>
    import Nav from '../components/Nav.svelte';

    export let segment;
</script>

<main class="relative bg-white overflow-hidden">

    <div class="flex flex-col h-screen">
        <div class="relative pt-6">
            <Nav {segment} />
        </div>
        <slot />
    </div>
</main>
