<script>
    import { fade } from "svelte/transition";
    import { NavItems } from "../Constants";

    export let content;
    const scrollToTopMessage = "Back to Top";
    let scroll = 0;
    let mobileMenu = false;

    const scrollToTop = () => {
        window.scroll(0, 0);
        if (mobileMenu) {
            mobileMenu = !mobileMenu;
        }
    };

    const handleNavClick = (item) => {
        document.getElementById(item).scrollIntoView();
        if (mobileMenu) {
            mobileMenu = !mobileMenu;
        }
    };

    // Toggles the mobile menu.
    const handleMobileMenuClick = () => {
        mobileMenu = !mobileMenu;
    };
</script>

<svelte:window bind:scrollY={scroll}></svelte:window>

<div style="--nav-items: {mobileMenu ? scroll > 0 ? content.length + 2 : content.length + 1 : 1}" 
    class="nav {scroll > 0 ? "shadow" : ""} {mobileMenu ? 'responsive' : ''}">
    <div class="stylebar"></div>
    <ul>
        <li class="icon" on:click={handleMobileMenuClick}>Menu</li>
        {#if scroll > 0}
            <li transition:fade={{duration: 200}} on:click={scrollToTop}>{scrollToTopMessage}</li>
        {/if}
        {#each content as item}
            <li on:click={() => handleNavClick(item)}>{item}</li>
        {/each}
    </ul>
</div>

<style>
:root {
    --nav-height: 50px;
    --nav-items: 1;
}

@media screen and (max-width: 800px) {
	.nav li {display: none;}
	.nav li.icon {
		float: right;
		display: block;
    }
    
    .nav.responsive {
        height: calc(var(--nav-height) * var(--nav-items));
    }

	.nav.responsive ul {
        display: block;
    }
    
	.nav.responsive li {
        opacity: 0;
		float: none;
		display: block;
        text-align: right;
        animation: fadeIn 1s forwards;
    }
}

.nav {
	transition: var(--quick-transition);
    background-color: var(--color-background);
    height: var(--nav-height);
    z-index: 9999;
    position: fixed;
    width: 100%;
    top: 0;
}

.nav .stylebar {
    height: 2px;
    width: 100%;
    background-color: var(--color-one);
}

.nav ul {
    margin: 0;
	padding: 0;
	list-style-type: none;
    display: flex;
    float: right;
	/* height: calc(var(--nav-height) * var(--nav-items)); */
}

.nav li {
    text-align: right;
    color: var(--color-text-one);
	font-family: 'Raleway', sans-serif;
    font-size: 1em;
    font-weight: 100;
    padding: 15px 15px;
	transition: var(--quick-transition);
}

.nav li:hover {
	transition: var(--quick-transition);
	cursor: pointer;
    color: var(--color-one);
    padding: 15px 20px;
}

.nav .icon {
	display: none;
}
</style>