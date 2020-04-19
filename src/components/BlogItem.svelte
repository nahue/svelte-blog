<script>
    import { fade } from 'svelte/transition';
    import Date from '../components/Date.svelte';

    export let post;
    let showMetadata = true;
</script>

<article
    on:mouseenter={() => (showMetadata = true)}
    on:mouseleave={() => (showMetadata = false)}>
    <a href={`/posts/${post.permalink}`}>
        <h3 class="mt-2 text-xl leading-10 font-semibold text-gray-900">
            {post.title}
            {#if showMetadata}
                <span
                    transition:fade
                    class="inline-flex items-center px-3 py-0.5 rounded-full
                    text-xs font-medium leading-4 bg-gray-100 text-gray-800">
                    {post.category}
                </span>
            {/if}
        </h3>
        <p class="text-sm leading-5 text-gray-500">
            <Date date={post.date} />
        </p>
    </a>
</article>
