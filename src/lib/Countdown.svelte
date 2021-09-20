<script>
    let event = new Date('Sept 20, 2021 11:00:00').getTime();
    let now, distance = 0;
    let days, hours, minutes, seconds = 0
    let timer = setInterval(countDown, 1000)

    function countDown() {
        now = new Date().getTime();
        distance = event - now;

        days = Math.floor(distance / (1000 * 60 * 60 * 24));
        hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
        minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
        seconds = Math.floor((distance % (1000 * 60)) / 1000);

        if(distance < 0) {
            clearInterval(timer)
        }

    }

    

</script>
{#if distance < 0}
<h2 class="missed-event">You've Missed The Event!</h2>
<p>Check Back Soon To Make Sure You Don't Miss The Next One</p>

{:else if !days}
<section class="count-section">
    <h2 class="countdown">0<span>d</span></h2>
    <h2 class="countdown">0<span>h</span></h2>
    <h2 class="countdown">0<span>m</span></h2>
    <h2 class="countdown">0<span>s</span></h2> 
</section>

{:else}
<div class="message">
    <a href="/reservation" class="checkout-button">Reserve Spot</a>

    <h2>Clock's Ticking</h2>
    <p>If there was ever a room you wanted to be in, this is it!</p>
    <p>Hurry before time expires...</p>
</div>
<section class="count-section">
    <h2 class="countdown">{days < 10 ? "0" + days : days}<span>d</span></h2>
    <h2 class="countdown">{hours < 10 ? "0" + hours : hours}<span>h</span></h2>
    <h2 class="countdown">{minutes < 10 ? "0" + minutes : minutes}<span>m</span></h2>
    <h2 class="countdown">{seconds < 10 ? "0" + seconds : seconds}<span>s</span></h2> 
</section>
{/if}

<style>
    .message {
        text-align: center;
    }

    .message h2 {
        color: var(--red);
        margin-top: 1.5em;
    }

    .checkout-button {
        background-image: var(--gradient);
        border-radius: 8px;
        color: var(--white);
        font-size: 1.2em;
        text-transform: uppercase;
        padding: 1em 3em;
        white-space: nowrap;
        transition: cubic-bezier(.79,.01,.48,1) 100ms;
    }

    .count-section {
        display: flex;
        justify-content: space-evenly;
        gap: 2em;
    }

    .countdown {
        position: relative;
    }

    .countdown::before {
        position: absolute;
        top: 0;
        left: 0;
        content: "";
        height: 100%;
        width: 100%;
        padding: 0.8em;
        background-color: var(--red);
        transform: translate(-25%, -35%);
        clip-path: circle();
        z-index: -1;
    }

    .missed-event {
        color: var(--red);
    }

    span {
        color: var(--dark);
    }

    @media(max-width: 380px) {
        .checkout-button {
            font-size: smaller;
        }
    }
</style>