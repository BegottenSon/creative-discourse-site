<script>
    import icon from './Icon.svg';
</script>

<header>
    <nav>
        <a sveltekit:prefetch href="/" id="icon"><img src={icon} alt="Begotten Sounds Icon"></a>
    </nav>
</header>

<style>
    header {
        margin-block: 1.5em;
    }

    nav {
        display: flex;
        align-items: center;
        justify-content: center;
    }

    img {
        height: 2.5em;
    }
</style>