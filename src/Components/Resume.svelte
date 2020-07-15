<script>
    export let content;
    let component;
    let scroll;
    let inView = false;
    let animation = false;
    $: inView = component && scroll + window.innerHeight > scroll + component.getBoundingClientRect().top * 1.5;
    $: if (inView) {
        animation = true;
    }
</script>

<svelte:window bind:scrollY={scroll}></svelte:window>

<div bind:this={component} class="center">
    <div id="Experience" class="container">
        <h1 style="--delay: 0.25s" class="{animation ? "fade-in" : ""}">Experience</h1>
        {#each content as section, index}
            <div style="--delay: {0.25 * (index + 2)}s" 
            class="shadow resume {animation ? "fade-in" : ""}">
                <div class="shadow image-container">
                    <img src="images/{section.Image}" alt="{section.Image}"/>
                </div>
                <div class="content">
                    <h2><strong>{section.Title}</strong> | {section.Subtitle}</h2>
                    <h3>{section.Position}</h3>
                    <ul>
                        {#each section.Content as item}
                            <li>{item}</li>
                        {/each}
                    </ul>
                </div>
            </div>
        {/each}
    </div>
</div>

<style>
    @media screen and (max-width: 800px) {
        .content {
            padding-top: 10px!important;
            text-align: center;
            border-left: none!important;
        }

        .content ul {
            padding: 10px;
            list-style-type: none;
        }

        .content li {
            text-align: left;
            padding: 0 10px; 
            margin: 5px 0;
            border-left: 1px solid var(--color-one)
        }

        .resume {
            flex-wrap: wrap;
        }
    }

    h1 {
        opacity: 0;
        margin: 20px 0;
        margin-top: 70px;
        text-align: center;
    }

    .container {
        width: 100%;
    }

    .resume {
        opacity: 0;
        display: flex;
        align-items: center;
        justify-content: center;
        border: white solid 1px;
        border-radius: 2px;
        padding: 10px;
        margin: 10px 0;
    }

    .resume:hover {
        transition: var(--quick-transition);
        transform: scale(1.05);
    }

    .content {
        padding: 0 10px;
        margin: 0 10px;
        color: var(--color-text-one);
        border-left: solid 1px var(--color-one);
        width: 100%;
    }

    .content h2,
    .content h3 {
        margin: 0;
    }

    .fade-in {
        --delay: 1s;
        animation: fadeInFromLeft 1s forwards var(--delay);
    }
</style>