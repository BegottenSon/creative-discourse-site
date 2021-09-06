<script>
    import { onMount } from "svelte";
    const keys = [
        {pianoKey: 'cPiano', song:'../static/media/Allstar1.mp3', transform: 'matrix(0.970948,0,0,1,10.2117,0)'},
        {pianoKey: 'dPiano', song:'../static/media/Reality.mp3', transform: 'matrix(0.970948,0,0,1,30.2117,0)'},
        {pianoKey: 'ePiano', song:'../static/media/Vibe.mp3', transform: 'matrix(0.970948,0,0,1,50.2117,0)'},
        {pianoKey: 'fPiano', song:'', transform: 'matrix(0.970948,0,0,1,70.2117,0)'},
        {pianoKey: 'gPiano', song:'', transform: 'matrix(0.970948,0,0,1,90.2117,0)'},
        {pianoKey: 'aPiano', song:'', transform: 'matrix(0.970948,0,0,1,110.212,0)'},
        {pianoKey: 'bPiano', song:'', transform: 'matrix(0.970948,0,0,1,130.212,0)'},    
    ]

    onMount(() => {
        // keys.forEach(strobe)
        strobe()
    })

    let windowAudio;

    function strobe() {
        let pianoLoad = Array.from(document.getElementsByTagName("rect"));
        let time = 100;
        for(let k = 0; k < 7; k++) {
            let key = pianoLoad[k];
            key.style.animationName = 'strobe';
            key.style.animationDelay = `${time}ms`;
            time += 80
        }
    }

    function playSong(e) {        
        let keyID = e.target.id;
        let targetKey = keys.find(key => key.pianoKey == keyID);
        if(targetKey.song){
            let song = new Audio(targetKey.song);
                song.play();
                windowAudio = song;
        }
    }

    function pauseSong() {
        if(windowAudio) windowAudio.pause()
    }
</script>

<svelte:window on:mousedown={pauseSong}/>

<svg width="100%" height="100%" viewBox="0 0 305 154" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:space="preserve" xmlns:serif="http://www.serif.com/" style="fill-rule:evenodd;clip-rule:evenodd;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:1.5;">
    <g transform="matrix(1,0,0,1,-881,-124)">
        <g id="Piano" transform="matrix(2.15631,0,0,2.17666,124.595,-733.649)">
            {#each keys as key}
            <g transform={key.transform}>
                <rect  id={key.pianoKey} on:click={playSong} x="351.493" y="394.558" width="20.598" height="69.346" style="stroke:black;stroke-width:0.94px;"/>
            </g>  
            {/each}
            <g transform="matrix(0.75,0,0,0.994438,92.8733,16.0376)">
                <rect x="361.493" y="380.638" width="20" 
                height="35.196" style="fill:rgb(26,26,26);stroke:black;stroke-width:1.05px;"/>
            </g>
            <g transform="matrix(0.75,0,0,0.994438,152.873,16.0376)">
                <rect x="361.493" y="380.638" width="20" 
                height="35.196" style="fill:rgb(26,26,26);stroke:black;stroke-width:1.05px;"/>
            </g>
            <g transform="matrix(0.75,0,0,0.994438,112.873,16.0376)">
                <rect x="361.493" y="380.638" width="20" 
                height="35.196" style="fill:rgb(26,26,26);stroke:black;stroke-width:1.05px;"/>
            </g>
            <g transform="matrix(0.75,0,0,0.994438,172.873,16.0376)">
                <rect x="361.493" y="380.638" width="20" 
                height="35.196" style="fill:rgb(26,26,26);stroke:black;stroke-width:1.05px;"/>
            </g>
            <g transform="matrix(0.75,0,0,0.994438,192.873,16.0376)">
                <rect x="361.493" y="380.638" width="20" 
                height="35.196" style="fill:rgb(26,26,26);stroke:black;stroke-width:1.05px;"/>
            </g>
        </g>
    </g>
</svg>

<style>
    g >rect:hover {
        fill: var(--link-hover);
    }

    g > rect:active {
    fill: var(--red);
    }

    rect {
        fill: var(--white);
        /* animation-name: strobe; */
        animation-duration: 3.3s ;
    }

    @keyframes hi {
        to {
            fill: var(--red)
        }
    }

    @keyframes strobe {
        0%, 20%, 40%, 60%, 80%, 100% {
            fill: var(--red);
        }
        10%, 30%, 50%, 70%, 90% {
            fill: var(--white);
        }
    }
</style>