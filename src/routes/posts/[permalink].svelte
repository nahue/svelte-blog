<script context="module">
    import { findPost } from '../../posts';

    export function preload(page) {
        return { post: findPost(page.params.permalink) };
    }
</script>

<script>
    export let post;
</script>

<svelte:head>
    <title>{post.title}</title>
</svelte:head>

<div class="w-full overflow-auto">
    <section
        class="w-full h-full mx-auto mt-20 px-0 lg:w-1/2 sm:w-1/2 xs:px-10">
        <article>
            <h3 class="flex-grow text-xl leading-4 text-gray-900">
                <span class="font-semibold">{post.title}</span>
            </h3>

            <div class="mt-10">
                {@html post.html}
            </div>
        </article>
    </section>
</div>
