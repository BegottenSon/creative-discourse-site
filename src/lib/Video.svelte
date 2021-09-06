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

<style>
    video {
        border-radius: 12px;
        box-shadow: rgba(70, 70, 2, 0.548) 2px 2px 25px;
        cursor: pointer;
        width: 100%;
    }
</style>