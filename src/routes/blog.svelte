<script>
    import { posts } from '../posts';
    import BlogItem from '../components/BlogItem.svelte';
</script>

<section class="w-1/2 m-auto">
    {#each posts as post}
        <BlogItem {post} />
    {/each}
</section>
