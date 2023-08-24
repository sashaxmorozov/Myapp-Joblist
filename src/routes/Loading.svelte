<script>
    import { loading } from '/Users/aleksandr/next-bootcamp/front-end/svelte-tailwind-app/myapp/src/stores/loading,js'
</script>

{#if $loading}
<div/>
{/if}

<style>
    div {
        --size: 60px;
        position: fixed;
        top: 0;
        left: 0;
        background: gray ;
        inset: calc(50%);
        border-radius: var(--size);
        height: var(--size);
        width: var(--size);
        animation: Loader 1s infinite alternate;
    }
    @keyframes Loader {
     from {
            transform: translate3d(100px, 0, 0);
        }
    to {
        transform: translate3d(-100px, 0 ,0);
    }
    }


</style>