<script>
    export let content;
    let component;
    let scroll;
    let inView = false;
    let animation = false;
    $: inView = component && scroll > component.getBoundingClientRect().top;
    $: if (inView) {
        animation = true;
    }
</script>

<svelte:window bind:scrollY={scroll}></svelte:window>

<div id="Contact" class="container">
    {#each content as icon}
        <a href="{icon.Link}" target="_blank">
            <div class="icon">
                <div class="image">
                    <img src="images/{icon.Image}" alt={icon.Image}/>
                </div>
            </div>
        </a>
    {/each}
</div>

<style>
    .container {
        width: 100%;
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: center;
    }

    .icon {
        margin: 10px;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }

    .image {
        height: 50px;
        width: 50px;
        background-color: white;
        border-radius: 2px;
        transition: var(--quick-transition);
    }

    .image img {
        height: 100%;
        width: 100%;
        object-fit: contain;
        z-index: 2;
    }

    .icon:hover .image {
        transform: translate(0, -20px);
        transition: var(--quick-transition);
    }

    .icon:hover .text {
        opacity: 1;
        transform: translate(0, -20px);
        transition: var(--quick-transition);
    }

    .text {
        opacity: 0;
        transition: var(--quick-transition);
        transform: translate(0, -40px);
        text-align: center;
        z-index: 1;
    }
</style>