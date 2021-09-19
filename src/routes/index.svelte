<script>
    import Title from "$lib/CDtitle.svelte";
    import Countdown from "$lib/Countdown.svelte";
    import Piano from "$lib/Piano.svelte";
    import Video from "$lib/Video.svelte";
</script>
<svelte:head>
    <title>Creative Discourse</title>
</svelte:head>

<section id="title" aria-label="Creative Discoure" title="Creative Discourse">
    <Title />
</section>

<section id="piano" aria-label="A Playable Piano">
    <Piano />
</section>

<section class="video">
    <Video clip="/media/Creative-Discourse-Promo.mp4"
        overlay="/media/CDoverlay-video.gif"
    />
</section>

<section id="countdown">
    <Countdown />
</section>

<style>
    section {
        margin-block: 1em;
    }

    #title {
        grid-column: 1/3;
        grid-row: 1;
        width: 40vw;
    }

    #piano {
        grid-column: 4/6;
        grid-row: 1;

    }
    .video {
        grid-column: 2/5;
        grid-row: 2;
        margin-block-end: 3.5em;
    }

    #countdown {
        grid-column: 2/5;
        grid-row: 3;
    }

    @media(max-width: 600px) {
        #title {
            width: 100%;
        }
    }
</style>
