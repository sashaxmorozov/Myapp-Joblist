<script>
import { logIn } from "../stores/store.js";
import { logOut } from "../utils/auth.js";
import { goto } from "$app/navigation";

function goToLogin() {
    goto('/login');
}
</script>


{#if $logIn} 
<button class="btn btn-md" on:click={logOut}> Logout </button>
<!-- {/if} -->
<!-- {#if $logIn === false} -->
{:else}
<button class="btn btn-md" on:click={goToLogin}> Login/Signup </button>
{/if}