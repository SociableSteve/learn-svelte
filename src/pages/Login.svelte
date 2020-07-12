<script>
    import Something from "../components/Something.svelte";

    let email;
    let password;

    import {createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();

    const ATTEMPT_LOGIN = `
    mutation authenticate($email: String!, $password: String!) {
        authenticate(email: $email, password: $password) {
            token
        }
    }
    `

    async function handleForm() {
        const body = {
            query: ATTEMPT_LOGIN,
            variables: {email, password}
        }

        const response = await fetch('https://www.madhouseminers.com/graphql', {
            headers: {
                'Content-Type': 'application/json'
            }, method: 'POST', body: JSON.stringify(body)
        });
        const data = await response.json();
        dispatch('login', data.data.authenticate.token);
    }
</script>

<style>
    p { color: red; font-size: 2em; }
</style>

<p>
    this is a P
</p>
<Something />

<form method="post" on:submit|preventDefault={handleForm}>
    <label for="email">E-mail Address</label>
    <input type="email" name="email" id="email" bind:value={email} required />

    <label for="password">Password Address</label>
    <input type="password" name="password" id="password" bind:value={password} required />

    <button type="submit">Log In</button>
</form>