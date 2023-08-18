<script>
    import { authenticateUser } from "/Users/aleksandr/next-bootcamp/front-end/svelte-tailwind-app/myapp/src/utils/auth.js";
    import { goto } from "$app/navigation";
    let formErrors = {};

  async function handleLogin(evt){
    evt.preventDefault();
    let username = evt.target['username'].value;
    let password = evt.target['password'].value;
    const success = await authenticateUser(username, password);
    if (success.success) {
        goto ("/") };

 }
</script>

<h1 class="text-center text-xl">Login</h1>

<div class="text-center">
    <a class="link-hover italic text-xs" href="/users/new"
        >Don't have an account? Click here to sign up.</a
    >
</div>
<div class="flex justify-center items-center mt-8">
    <form on:submit={handleLogin} class="w-1/3">
        <div class="form-control w-full">
            <label class="label" for="username">
                <span class="label-text">Username</span>
            </label>
            <input
                type="text"
                name="username"
                placeholder="johndoe"
                class="input input-bordered w-full"
            />
            {#if 'username' in formErrors}
                <label class="label" for="username">
                    <span class="label-text-alt text-red-500">{formErrors['username'].message}</span>
                </label>
            {/if}
        </div>
        <div class="form-control w-full">
            <label class="label" for="password">
                <span class="label-text">Password</span>
            </label>
            <input
                type="password"
                name="password"
                placeholder=""
                class="input input-bordered w-full"
                required
            />
            {#if 'password' in formErrors}
                <label class="label" for="password">
                    <span class="label-text-alt text-red-500">{formErrors['password'].message}</span>
                </label>
            {/if}
        </div>
        <div class="form-control w-full mt-4">
            <button class="btn btn-md">Login</button>
        </div>
    </form>
</div>


