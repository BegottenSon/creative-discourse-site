<script>
    import { dripKey } from "./Env";
    import { formComplete } from "./complete.js";
    // import * as client from "drip-nodejs";
    // let drip = client({ token: dripKey, accountId: 2600038 });
    
    let firstName, lastName, email, skill = "";

    async function sendForm() {
        const postAPI = `https://api.getdrip.com/v2/${dripKey}`;
        let data = {
            "first_name": firstName,
            "last_name": lastName,
            "email": email,
            "pro_skill": skill
        }
        const response = await fetch(postAPI, {
            method: "POST",
            headers: { 'Content-Type': 'application/json'},
            body: JSON.stringify(data)
        });
        let content = await response.json();
        console.log(content);
    }
    
    // async function sendForm() {
    //     let data = {
    //         "first_name": firstName,
    //         "last_name": lastName,
    //         "email": email,
    //         "pro_skill": skill
    //     }
    //     drip.createUpdateSubscriber(data).then((response) => {console.log(response)})

    // }

    function handleForm() {
        if(firstName && email) {
            $formComplete = true;
            sendForm()
        }
        return false
    }
</script>
<section id="drip-section">
    <form action="https://www.getdrip.com/forms/117453377/submissions" method="post" data-drip-embedded-form="117453377" id="drip-ef-117453377">
      <div data-drip-attribute="description"><strong>Sign Up Below to Let Us Know You're Coming!</strong><br>
      </div>
      
      <div>
          <label for="drip-first-name">First Name</label><br>
          <input type="text" id="drip-first-name" name="fields[first_name]" bind:value={firstName} placeholder="First Name">
      </div>
    
      <div>
          <label for="drip-last-name">Last Name</label><br>
          <input type="text" id="drip-last-name" name="fields[last_name]" bind:value={lastName} placeholder="Last Name">
      </div>
    
      <div>
          <label for="drip-email">Email Address</label><br>
          <input type="email" id="drip-email" name="fields[email]" bind:value={email} placeholder="Your Best Email">
      </div>
    
      <div>
          <label for="drip-pro-skill">Choose Your Skill</label><br>
          <select name="fields[pro_skill]" class="drip-select" bind:value={skill}>
            <option disabled="" selected="" value="">Choose Your Skill</option>
              <option value="Producer">Producer</option>
              <option value="Artist">Artist</option>
              <option value="Both">Both</option>
          </select>
      </div>
    
      <div style="display: none;" aria-hidden="true">
        <label for="website">Website</label><br>
        <input type="text" id="website" name="website" tabindex="-1" autocomplete="false" value="">
      </div>

      <div>
        <input type="submit" value="Next Step" data-drip-attribute="sign-up-button" id="drip-button" on:click|preventDefault={handleForm}>
      </div>
    </form>  
  </section>

<style>
    #drip-section {
        border: var(--red) solid 2px;
        border-radius: 8px;
        margin-bottom: 1em;
        padding: 0.4em;
        width: 100%;
        font-family: 'Helvetica';
    }

    form {
        display: grid;
        place-items: center;
    }

    #drip-ef-117453377 > div {
        margin-bottom: 0.7em;
    }

    #drip-button {
    font-size: 1em;
    padding: 0.7em;
    width: max-content;
    font-weight: 500;
    color: var(--white);
    background-color: var(--red);
    background-image: var(--gradient);
    border: none;
    border-radius: 8px;
    font-family: 'Helvetica', sans-serif;
    cursor: pointer;
    transition: ease 0.1s;
    }

    input::-webkit-outer-spin-button {
        -webkit-appearance: none;
    }

    input[type=text], input[type=email] {
        border: 1px solid var(--red);
        border-radius: 4px;
        background-color: var(--grey);
        color: var(--white);
    }

    ::placeholder {
        color: var(--white);
    }

    .drip-select {
        position: relative;
        margin-bottom: 1em;
        padding: 0.5em;
        border: none;
        border-color: var(--red);
        border-radius: 4px;
        background-color: var(--red);
        color: var(--white);
    }
</style>