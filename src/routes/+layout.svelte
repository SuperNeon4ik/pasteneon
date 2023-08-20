<script>
    import Header from "./Header.svelte";
    import { onMount } from 'svelte';
    import { theme } from '$lib/theming.js';
    import Cookies from 'js-cookie';

    let currentTheme = "light";

    const cookieThemeValue = Cookies.get('theme');
    if (cookieThemeValue !== undefined) {
        currentTheme = cookieThemeValue;
        document.documentElement.dataset.theme = currentTheme;
        theme.set(currentTheme);
    }

    onMount(() => {
        theme.subscribe(value => {
            currentTheme = value;
            document.documentElement.dataset.theme = value;
            Cookies.set('theme', value, { expires: 365, sameSite: "Lax" });
        });

        document.documentElement.dataset.theme = currentTheme;
    });
</script>

<Header/>
<slot />