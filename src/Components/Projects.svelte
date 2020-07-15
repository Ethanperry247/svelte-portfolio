<script>
import { onMount } from "svelte";


    export let content;
    let component;
    let scroll;
    let inView = false;
    let animation = false;
    $: inView = component && scroll + window.innerHeight * 1.5 > scroll + component.getBoundingClientRect().top;
    $: if (inView) {
        animation = true;
    }
</script>

<svelte:window bind:scrollY={scroll}></svelte:window>

<div id="Projects" class="center">
    <h1  class="{animation ? "fade-in" : ""}">Projects</h1>
    <div class="container">
        {#each content as section, index}
            <div bind:this={component}
                style="--delay: {0.25 * (2 + index)}s"
                class="shadow projects {animation ? "fade-in" : ""}">
                <div class="image">
                    <img src="images/mountain.jpg" />
                </div>
                <div class="content">
                    <h2>{section.Title}</h2>
                    {#each section.Content as paragraph}
                        <p>{paragraph}</p>
                    {/each}
                    <div class="tags">
                        {#each section.Tags as tag}
                            <p>{tag}</p>
                        {/each}
                    </div>
                </div>
            </div>
        {/each}
    </div>
</div>

<style>
    @media screen and (max-width: 800px) {
        .projects {
            width: 100%!important;
        }
    }

    h1 {
        width: 100%;
        opacity: 0;
        margin: 20px 0;
        margin-top: 70px;
        text-align: center;
    }

    .container {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
    }

    .projects {
        opacity: 0;
        width: 45%;
        margin: 20px 0;
        border-radius: 2px;
        background-color: var(--color-white);
    }

    .projects .image {
        width: 100%;
        margin: 0;
    }

    .projects .image img {
        width: 100%;
        height: 100%;
        object-fit: contain;
        border-top-left-radius: 2px;
        border-top-right-radius: 2px;
    }

    .projects .content {
        padding: 10px;
    }

    .projects .content h2, 
    .projects .content p {
        color: var(--color-background);
    }

    .projects .content h2 {
        margin-top: 0;
    }

    .projects .tags {
        display: flex;
        flex-wrap: wrap;
    }

    .projects .tags p {
        margin: 0 5px 5px 0;
        padding: 2px;
        border: solid 1px var(--color-one);
        border-radius: 2px;
        color: var(--color-one);
        transition: var(--quick-transition);
    }

    
    .projects .tags p:hover {
        color: var(--color-two);
        transition: var(--quick-transition);
        border: solid 1px var(--color-two);
    }

    .fade-in {
        --delay: 0.25s;
        animation: fadeInFromBelow 1s forwards var(--delay);
    }
</style>