<script>
import { logIn } from "../stores/store.js";
import { logOut } from "../utils/auth.js";
import { goto } from "$app/navigation";

function goToLogin() {
    goto('/login');
}
function goToMain() {
    goto('/');
}
function goToJobForm()
{goto('/jobs/new')
}
</script>


{#if $logIn} 
<button class="btn btn-md" on:click={logOut}> Logout </button>
{:else}
<button class="btn btn-md" on:click={goToLogin}> Login </button>
{/if}

<button class="btn btn-md" on:click={goToMain}> Main </button>
{#if $logIn}
<button class="btn btn-md" on:click={goToJobForm}> Post a job </button>
{/if}
