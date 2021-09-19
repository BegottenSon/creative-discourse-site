<script>
    import { loadStripe } from "@stripe/stripe-js";
    import { testKey, KEY, discoursePrice } from "$lib/Env";
    import { formComplete } from "./complete.js";

    let disableSection = true;
    let disableButtons = true;

    const enableSection = formComplete.subscribe(value => {
        disableSection = !value
        disableButtons = !value
    })

    let DOMAIN = new URL('https://begotten.live');
    // let PRICE_ID = discoursePrice;
    let PRICE_ID = "price_1HCFth4KI0G6StnQH7TEFW3Z"; //TEST PRICE
    let minRESERVATION = 1;
    let maxRESERVATION = 10;
    let reservationCounter = 10;
    let total = 40;
    let showError = false;
    let quantityInput = 1;

    function handleSubtract() {
        quantityInput -= 1
        if(quantityInput <= minRESERVATION) {
            quantityInput = minRESERVATION;
        }
        total = 40 * quantityInput
    }

    function handleAdd() {
        quantityInput += 1
        if(quantityInput >= maxRESERVATION) {
            quantityInput = maxRESERVATION;
        }
        total = 40 * quantityInput
    }

    // Handle any errors from Checkout and Update Reservation Counter
    let handleResult = (result) => {
        if(result.error) {
            showError = true;
            }
            reservationCounter -= 1;
    }

    //Handle Buy Button
    async function checkoutRedirect() {
        const stripe = await loadStripe(testKey)
        let quantity = quantityInput;
        stripe.redirectToCheckout({
            mode: 'payment',
            lineItems: [{price: PRICE_ID, quantity: quantity}],
            successUrl: DOMAIN + "success.html?session_id={CHECKOUT_SESSION_ID}",
            cancelUrl: DOMAIN + "reservation"
        }).then(handleResult)
    }

</script>

<section id="buy-section" class:disableSection>
    <h4 id="buy-header">How Many Are Pulling Up?</h4>
    <div class="quantity-setter">
      <button class="increment-btn" id="subtract" on:click={handleSubtract}>
        -
      </button>
      <input type="number" id="quantity-input" min="1" bind:value={quantityInput} />
      <button class="increment-btn" id="add" on:click={handleAdd}>
        +
      </button>
    </div>
    <p class="sr-legal-text">Number of Reservations (max {maxRESERVATION})</p>

    <button class="button" id="buyButton" on:click={checkoutRedirect} disabled={disableSection}>
      Buy for $<span id="total">{total}</span>.00
    </button>
    {#if showError}
        <div id="error-message">
            <p>
            Uh Ohh! Reservations going like hotcakes. All spots may have been 
            reserved or another error has occured.
            </p>
        </div>
    {/if}
</section>

<style>
    .disableSection {
        filter: opacity(0.3);
    }
    #buy-section {
        display: grid;
        place-items: center;
        border: var(--red) solid 2px;
        border-radius: 8px;
        margin-bottom: 1em;
        padding: 0.4em;
        width: 100%;
        font-family: 'Helvetica';
    }

    #quantity-input {
        background-color: var(--white);
        padding: 0.3em;
        width: 100px;
        text-align: center;
        border-style: none;
        user-select: none;
        -moz-appearance: textfield;
    }

    #buyButton {
        font-size: 1em;
        padding: 1em;
    }

    #buyButton:disabled {
        background-image: none;
        background-color: var(--grey);
    }

    input[type=number] {
        -moz-appearance: textfield;
        appearance: none;
    }

    .increment-btn {
        padding: 0.02em 0.4em;
        background-image: none;
        color: var(--dark);
    }

    .sr-legal-text {
        font-size: 0.7em;
    }

</style>