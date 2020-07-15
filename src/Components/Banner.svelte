<script>
    export let content;
    export let height;
    export let scrollItem;

    const handleClick = () => {
        document.getElementById(scrollItem).scrollIntoView();
    };
</script>

<div style="height: {height / 2}px; padding: {height / 3}px 0;" class="banner">
    {#if content.image}
        <img class="shadow" src="images/{content.image}" alt="Author"/>
    {/if}
    {#if content.title}
        <h1>{content.title}</h1>
    {/if}
    {#if content.details}
        {#each content.details as detail}
            <p>{detail}</p>
        {/each}
    {/if}
    {#if content.title}
        <h1 on:click={handleClick} class="arrow">&#9660;</h1>
    {/if}
</div>

<style>
    .banner {
        text-align: center;
    }

    .banner h1 {
        color: var(--color-one);
	    text-emphasis: none;
	    margin: 10px 0;
        font-weight: 200;
    }

    .banner p {
        margin: 5px;
    }

    .banner img {
        object-fit: cover;
        height: 100px;
        width: 100px;
        object-position: 0 0;
        border-radius: 50%;
    }

    .arrow {
        animation: point 3s infinite;
        cursor: pointer;
    }

    @keyframes point {
        0% {transform: translate(0);}
        50% {transform: translate(0, 20px);}
        100% {transform: translate(0);}
    }
</style>