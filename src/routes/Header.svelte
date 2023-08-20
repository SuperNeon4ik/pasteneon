<script>
    let innerWidth = 0;
    let innerHeight = 0;

    $: desktopWindow = innerWidth * 1.5 > innerHeight;
    let hamDropdownShow = false;

    function toggleHamDropdown() {
        hamDropdownShow = !hamDropdownShow;
    }
</script>

<svelte:window bind:innerWidth bind:innerHeight />

<nav>
    <div class="logo">
        <h1>Paste<span id="fancy">Neon</span></h1>
    </div>
    <div class="desktop-menu" class:hide={!desktopWindow}>
        <a class="simple-button" href="https://superneon4ik.me">About</a>
        <a class="primary-button" href="#amongus">New Neon</a>
    </div>
    <button class="ham-menu" class:hide={desktopWindow} on:click={toggleHamDropdown}>
        <svg viewBox="0 0 32 32" xml:space="preserve" xmlns="http://www.w3.org/2000/svg" enable-background="new 0 0 32 32"><path d="M4 10h24a2 2 0 0 0 0-4H4a2 2 0 0 0 0 4zm24 4H4a2 2 0 0 0 0 4h24a2 2 0 0 0 0-4zm0 8H4a2 2 0 0 0 0 4h24a2 2 0 0 0 0-4z" fill="#030203" class="fill-000000"></path></svg>
    </button>
</nav>

<div class="ham-dropdown" class:show={!desktopWindow && hamDropdownShow}>
    <a class="primary">New Neon</a>
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

    #fancy {
        background: linear-gradient(120deg, var(--primary), var(--accent));
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
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
        background-color: #ded7e4;
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
        background-color: var(--primary);
    }
</style>