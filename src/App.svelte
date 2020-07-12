<script>
    import Login from "./pages/Login.svelte";

    let user;

    function loggedIn(token) {
        user = token.detail;
    }

    import Homepage from "./pages/Homepage.svelte";

    console.log(document.location.pathname);
</script>

{#if !user}
<Login on:login={loggedIn} />
{:else}
<Homepage {user} />
{/if}