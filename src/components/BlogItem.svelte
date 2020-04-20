<script>
    import { fade } from 'svelte/transition';
    import Date from '../components/Date.svelte';

    export let post;
</script>

<article>
    <a href={`/posts/${post.permalink}`} class="flex items-center justify-between align-middle my-5">
        <span
            class="flex-none inline-flex items-center px-2 mx-2 py-0.5 rounded-full text-xs w-10
            font-medium leading-4 bg-gray-100 text-gray-800">
            {post.category}
        </span>
        <h3 class="flex-grow text-xl leading-4 text-gray-900">
            <span class="font-semibold">{post.title}</span>
        </h3>
        <p class="flex-none inline-flex text-sm leading-5 text-gray-500">
            <Date date={post.date} />
        </p>
    </a>
</article>
