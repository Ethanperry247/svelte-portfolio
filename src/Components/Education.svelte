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

<div class="center">
    <div id="Education" class="spotlight">
        <h1 class="{animation ? "fade-in" : ""}">Education</h1>
        <div class="shadow image image-container {animation ? "roll-and-fade" : ""}">
            <img src="images/{content.Image}"/>
        </div>
        <div bind:this={component} class="shadow content {animation ? "fade-right" : ""}">
            <h2><strong>{content.Title}</strong> | {content.Subtitle}</h2>
            <h3>{content.Position}</h3>
            <ul>
                {#each content.Content as item}
                    <li><strong>{item.split(":")[0]}</strong>:{item.split(":")[1]}</li>
                {/each}
            </ul>
        </div>
    </div>
</div>

<style>
    @media screen and (max-width: 800px) {
        .spotlight .content {
            margin: 0!important;
            width: 100%!important;
            text-align: center;
            padding: 80px 0!important;
        }

        .spotlight .image {
            margin: auto;
            left: 0!important;
        }

        .spotlight .content ul {
            padding: 10px;
            list-style-type: none;
        }

        .spotlight .content li {
            text-align: left;
            padding: 0 10px; 
            margin: 5px 0;
            border-left: 1px solid var(--color-one)
        }
    }

    h1 {
        margin: 0;
        margin-top: 70px;
        opacity: 0;
        text-align: center;
    }
    
    .spotlight {
        width: 100%;
    }

    .spotlight .content {
        opacity: 0;
        background-color: var(--color-white);
        margin: 0;
        max-width: 100%;
        margin: 0;
        border-radius: 2px;
        padding: 50px 60px;
        color: var(--color-background);
    }

    .spotlight .content h3,
    .spotlight .content h2 {
        margin: 0;
    }

    .spotlight .content li {
        color: var(--color-background);
        list-style-position: outside;
    }

    .spotlight .image {
        opacity: 0;
        position: relative;
        top: 65px;
        left: -35px;
    }

    .roll-and-fade {
        animation: fadeAndRollFromLeft 1s forwards 1s;
        z-index: 1;
    }

    .fade-right {
        animation: fadeInFromRight 1s forwards 0.5s;
        z-index: 0;
    }

    .fade-in {
        animation: fadeIn 1s forwards 1.5s;
    }
</style>