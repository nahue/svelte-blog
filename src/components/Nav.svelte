<script>
    export let segment;
    let isNavOpen = false;

    function handleClick(event) {
        isNavOpen = !isNavOpen;
    }
</script>

<nav
    class="relative max-w-screen-xl mx-auto flex items-center justify-between
    px-4 sm:px-6">
    <div class="flex items-center flex-1">
        <div class="flex items-center justify-between w-full md:w-auto">
            <div class="-mr-2 flex items-center md:hidden">
                <button
                    on:click={e => handleClick(e)}
                    class="inline-flex items-center justify-center p-2
                    rounded-md text-gray-400 hover:text-gray-500
                    hover:bg-gray-100 focus:outline-none focus:bg-gray-100
                    focus:text-gray-500 transition duration-150 ease-in-out">
                    <svg
                        class="h-6 w-6"
                        stroke="currentColor"
                        fill="none"
                        viewBox="0 0 24 24">
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M4 6h16M4 12h16M4 18h16" />
                    </svg>
                </button>
            </div>
        </div>
        <div class="hidden md:block">
            <a
                href="/"
                class:text-gray-900={segment === 'home'}
                aria-current={segment === 'home' ? 'page' : undefined}
                class="font-medium text-gray-300 hover:text-gray-900
                focus:outline-none focus:text-gray-900 transition duration-150
                ease-in-out">
                Home
            </a>
            <!--<a
                href="resume"
                aria-current={segment === 'resume' ? 'page' : undefined}
                class="ml-10 font-medium text-gray-300 hover:text-gray-900
                focus:outline-none focus:text-gray-900 transition duration-150
                ease-in-out">
                Resume
            </a>-->
            <a
                href="blog"
                aria-current={segment === 'blog' ? 'page' : undefined}
                class="ml-10 font-medium text-gray-300 hover:text-gray-900
                focus:outline-none focus:text-gray-900 transition duration-150
                ease-in-out">
                Blog
            </a>
        </div>
    </div>
    <!--
      Mobile menu, show/hide based on menu open state.

      Entering: "duration-150 ease-out"
        From: "opacity-0 scale-95"
        To: "opacity-100 scale-100"
      Leaving: "duration-100 ease-in"
        From: "opacity-100 scale-100"
        To: "opacity-0 scale-95"
    -->
    <div
        class="absolute top-0 inset-x-0 p-2 transition transform
        origin-top-right md:hidden"
        class:opacity-0={!isNavOpen}
        class:scale-75={!isNavOpen}>
        <div class="rounded-lg shadow-md">
            <div class="rounded-lg bg-white shadow-xs overflow-hidden">
                <div class="px-5 pt-4 flex items-center justify-between">
                    <div>
                        <img
                            class="h-8 w-auto"
                            src="/img/logos/workflow-mark-on-white.svg"
                            alt="" />
                    </div>
                    <div class="-mr-2">
                        <button
                            on:click={e => handleClick(e)}
                            class="inline-flex items-center justify-center p-2
                            rounded-md text-gray-400 hover:text-gray-500
                            hover:bg-gray-100 focus:outline-none
                            focus:bg-gray-100 focus:text-gray-500 transition
                            duration-150 ease-in-out">
                            <svg
                                class="h-6 w-6"
                                stroke="currentColor"
                                fill="none"
                                viewBox="0 0 24 24">
                                <path
                                    stroke-linecap="round"
                                    stroke-linejoin="round"
                                    stroke-width="2"
                                    d="M6 18L18 6M6 6l12 12" />
                            </svg>
                        </button>
                    </div>
                </div>
                <div class="px-2 pt-2 pb-3">
                    <a
                        href="/"
                        class="block px-3 py-2 rounded-md text-base font-medium
                        text-gray-700 hover:text-gray-900 hover:bg-gray-50
                        focus:outline-none focus:text-gray-900 focus:bg-gray-50
                        transition duration-150 ease-in-out">
                        Home
                    </a>
                    <!--<a
                        href="/resume"
                        class="mt-1 block px-3 py-2 rounded-md text-base
                        font-medium text-gray-700 hover:text-gray-900
                        hover:bg-gray-50 focus:outline-none focus:text-gray-900
                        focus:bg-gray-50 transition duration-150 ease-in-out">
                        Resume
                    </a>-->
                    <a
                        rel=prefetch
                        href="/blog"
                        class="mt-1 block px-3 py-2 rounded-md text-base
                        font-medium text-gray-700 hover:text-gray-900
                        hover:bg-gray-50 focus:outline-none focus:text-gray-900
                        focus:bg-gray-50 transition duration-150 ease-in-out">
                        Blog
                    </a>
                </div>
            </div>
        </div>
    </div>
</nav>
