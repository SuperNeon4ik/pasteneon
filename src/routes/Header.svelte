<script>
    import { onMount } from 'svelte';
    import { theme } from '$lib/theming.js';

    let currentTheme = "light";
    let innerWidth = 0;
    let innerHeight = 0;

    $: desktopWindow = innerWidth * 1.5 > innerHeight;
    let hamDropdownShow = false;

    function toggleHamDropdown() {
        hamDropdownShow = !hamDropdownShow;
    }

    function toggleDarkMode() {
        theme.set(currentTheme === "light" ? "dark" : "light");
    }

    onMount(() => {
        theme.subscribe(value => {
            currentTheme = value;
        });
    });
</script>

<svelte:window bind:innerWidth bind:innerHeight />

<nav>
    <a href="/" class="logo">
        <h1>Paste<span class="fancy-text">Neon</span></h1>
    </a>
    {#if innerWidth > 0 && innerHeight > 0}
    <div class="desktop-menu" class:hide={!desktopWindow}>
        <button class="theme-button" on:click={toggleDarkMode}>
            {#if currentTheme === "light"}
                <svg class="feather feather-sun" fill="none" stroke="var(--text)" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><circle cx="12" cy="12" r="5"></circle><path d="M12 1v2M12 21v2M4.22 4.22l1.42 1.42M18.36 18.36l1.42 1.42M1 12h2M21 12h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42"></path></svg>
            {:else}
                <svg viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg"><path d="M32 256C32 132.2 132.3 32 255.8 32c11.36 0 29.7 1.668 40.9 3.746 9.616 1.777 11.75 14.63 3.279 19.44C245 86.5 211.2 144.6 211.2 207.8c0 109.7 99.71 193 208.3 172.3 9.561-1.805 16.28 9.324 10.11 16.95C387.9 448.6 324.8 480 255.8 480 132.1 480 32 379.6 32 256z" fill="var(--text)" class="fill-000000"></path></svg>
            {/if}
        </button>
        <a class="simple-button" href="https://superneon4ik.me">About</a>
        <a class="primary-button" href="/new">New Neon</a>
    </div>
    <button class="ham-menu" class:hide={desktopWindow} on:click={toggleHamDropdown}>
        <svg viewBox="0 0 32 32" xml:space="preserve" xmlns="http://www.w3.org/2000/svg" enable-background="new 0 0 32 32"><path d="M4 10h24a2 2 0 0 0 0-4H4a2 2 0 0 0 0 4zm24 4H4a2 2 0 0 0 0 4h24a2 2 0 0 0 0-4zm0 8H4a2 2 0 0 0 0 4h24a2 2 0 0 0 0-4z" fill="var(--text)" class="fill-000000"></path></svg>
    </button>
    {/if}
</nav>

<div class="ham-dropdown" class:show={!desktopWindow && hamDropdownShow}>
    <a href="/new" class="primary">New Neon</a>
    <a href="https://superneon4ik.me">About</a>
</div>

<style>
    nav {
        margin: 0 3em;
        text-align: center;
        display: flex;
        align-content: center;
        justify-content: space-between;
        align-items: center;
    }
    nav > a {
        color: var(--text);
        text-decoration: none;
    }

    .desktop-menu {
        display: flex;
        flex-direction: row;
        justify-content: flex-end;
        align-items: center;
    }

    .ham-menu {
        all: unset;
        width: 2em;
        height: 2em;
    }

    .hide {
        display: none;
    }

    .ham-dropdown {
        width: 100%;
        height: max-content;
        max-height: 0;
        transition: max-height 200ms ease-in-out;
        overflow: hidden;
        display: flex;
        flex-direction: column;
        background-color: rgba(222, 215, 228, 0.11);
    }
    .ham-dropdown.show {
        max-height: 500px;
    }

    .ham-dropdown > a {
        color: var(--text);
        text-decoration: none;
        padding: 1em 2em;
    }
    .ham-dropdown > a.primary {
        background: linear-gradient(120deg, var(--primary), var(--accent));
    }

    .theme-button {
        all: unset;
        width: 2em;
        height: 2em;
    }
    .theme-button > svg {
        width: 100%;
        height: 100%;
    }
</style>