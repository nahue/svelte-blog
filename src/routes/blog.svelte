<script>
    import { posts } from '../posts';
    import BlogItem from '../components/BlogItem.svelte';
</script>

<section class="w-full mx-auto my-auto px-0 lg:w-1/2 sm:w-1/2 xs:px-10">
    {#each posts as post}
        <BlogItem {post} />
    {/each}
</section>
