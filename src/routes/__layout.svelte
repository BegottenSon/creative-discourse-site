<script>
    import '../app.css';
    import Header from "$lib/Header/index.svelte"
</script>
<Header />
<main>
    <slot></slot>
</main>

<style>
    main {
        display: grid;
        grid-template-columns: repeat(5, 1fr);
        margin: 0em 4em 1em 4em;
    }

    @media (max-width: 600px) {
        main {
            display: flex;
            flex-direction: column;
        }
    }
</style>