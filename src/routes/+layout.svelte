<script>
    import Header from "./Header.svelte";
    import { onMount } from 'svelte';
    import { theme } from '$lib/theming.js';

    let currentTheme = "light";

    onMount(() => {
        theme.subscribe(value => {
            currentTheme = value;
            document.documentElement.dataset.theme = value;
        });

        document.documentElement.dataset.theme = currentTheme;
    });
</script>

<Header/>
<slot />