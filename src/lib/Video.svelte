<script>
    export let clip;
    export let overlay;
    let currentTime, muted;
    let paused = true;
    function handleMouseDown(e) {
        if(paused) {
            e.target.play()
        }else {
            e.target.pause()
        }
        if(window.$_currentlyPlaying && window.$_currentlyPlaying != e.target)
        window.$_currentlyPlaying.pause(); 
    }
</script>
<section>

    <video
    src={clip}
    poster={overlay}
    bind:currentTime
    bind:paused
    bind:muted
    on:mousedown={handleMouseDown}
    >
    <track kind="captions">
    </video>
</section>

<style>
    section {
        display: grid;
        place-items: center;
        border-radius: 12px;
        width: 100%;
        height: 110%;
        background-image: radial-gradient(#0f0e0e, #1a1a1a);
        box-shadow: inset 0 0 10px 1px rgb(12, 4, 9);
    }
    video {
        border-radius: 12px;
        cursor: pointer;
        width: 95%;
    }
</style>