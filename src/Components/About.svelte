<script>
    export let content;
    let scroll;
    let about;
    let inView = false;
    let animation = false;
    $: inView = about && scroll > about.getBoundingClientRect().top;
    $: if (inView) {
        animation = true;
    }
</script>

<svelte:window bind:scrollY={scroll}></svelte:window>

<div id="About" class="center">
    <div>
        <h1 class="{animation && "fade-in"}">{content.SectionTitle}</h1>
        <div bind:this={about} class="about">
            <div class="content {animation && "fade-left"}">
                {#each content.Content as paragraph}
                    <p>{paragraph}</p>
                {/each}
            </div>
            <div class="stylebar {animation && "fade-in"}"></div>
            <div class="image {animation && "fade-right"}">
                <img src="images/{content.Image}" alt="{content.Image}">
            </div>
        </div>
    </div>
</div>



<style>
    @media screen and (max-width: 800px) {
        .about {
            flex-direction: column;
            justify-content: center;
        }

        .about .content {
            width: 100%!important;
            text-align: center!important;
        }

        h1 {
            margin: 0;
        }

        .about .image {
            width: 100%!important;
        }

        .stylebar {
            margin: 10px 0!important;
            height: 1px!important;
            width: 100%!important;
        }

        .fade-left,
        .fade-right,
        .fade-in {
            animation: fadeInFromBelow 1s forwards 0.3s!important;
        }
    }

    h1 {
        opacity: 0;
        margin-top: 70px;
        text-align: center;
    }

    .about {
        display: flex;
        justify-content: space-evenly;
    }

    .about .content {
        opacity: 0;
        width: 50%;
        text-align: right;
    }

    .about .content :last-child {
        margin-bottom: 0;
    }

    .about .image {
        opacity: 0;
        width: 50%;
    }

    .about .image img {
        width: 100%;
        height: 100%;
        object-fit: contain;
    }

    .stylebar {
        opacity: 0;
        width: 1px;
        margin: 0 10px;
        background-color: var(--color-one);
    }

    .fade-in {
        animation: fadeIn 1s forwards 0.3s;
    }

    .fade-left {
        animation: fadeInFromLeft 1s forwards 0.3s;
    }

    .fade-right {
        animation: fadeInFromRight 1s forwards 0.3s;
    }
</style>