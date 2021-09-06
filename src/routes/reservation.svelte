<script>
import Checkout from "$lib/Checkout.svelte";
import Form from "$lib/Form.svelte";

</script>

<section class="info-section">
    <h1>Reserve Your Spot</h1>
    <p>
        Creative Discourse is an event where Creatives – 
        artists, producers, instrumentalists – 
        come together in one studio to make music. 
        The energy in the room being high and the creative 
        jucies flowing brings songs into existence that otherwise 
        wouldn't have spawned.
    </p>
</section>

<section class="reserve-form">
    <h1>Creative Discourse Reservation</h1>
    <p>Reserve your spot for the studio session. 
        Location of the studio will be in the email sent after registration
    </p>
    <p>Sept. 30th<br>
        11am-3pm
    </p>
    <p>
        <em>
        Payment section will be enabled after entering
        your info below.
        </em>
    </p>
    <img src="images/Creative Discourse.jpg" width="60%" alt="Creative Discourse Cover">
    <Form />
    <Checkout />

</section>

<style>
    .info-section {
        grid-column: 2/5;
    }

    .info-section > h1 {
        text-align: center;
    }

    .reserve-form {
        grid-column: 2/5;
        display: flex;
        flex-direction: column;
        align-items: center;
        border-radius: 20px;
        padding: 2em;
        background-color: var(--grey);
    }

    @media(max-width: 600px) {
        .reserve-form {
            width: 75vw;
            align-self: center;
        }
    }
</style>