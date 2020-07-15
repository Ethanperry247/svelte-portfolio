
<div class="logo">
    <div class="anim1"></div>
    <div class="anim2"></div>
    <p class="logo">E</p>
</div>

<style>
    .logo {
        top: 12.5px;
        left: 20px;
        text-align: center;
        position: absolute;
        z-index: 9999;
    }

    .logo div {
        position: absolute;
        border: 1px solid var(--color-one);
        border-radius: 50%;
        height: 30px;
        width: 30px;
    }

    div.anim1 {
        animation: rotate 4s linear infinite;
    }

    div.anim2 {
        animation: rotate2 6s linear infinite;
    }

    .logo p {
        font-family: 'Raleway', sans-serif;
        position: absolute;
        top: 7.5px;
        left: 11px;
        margin: 0;
        z-index: 0;
        color: var(--color-one);
    }

    @keyframes rotate {
        0% {transform: rotate(0);}
        100% {transform: rotate3d(1, 1, 1, 360deg);}
    }

    @keyframes rotate2 {
        0% {transform: rotate(0);}
        100% {transform: rotate3d(-1, 1, 0, 360deg);}
    }
</style>