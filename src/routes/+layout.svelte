<script> 
import "../app.css"
import Navbar from "./Navbar.svelte"
import { navigating } from '$app/stores'
import { loading } from "../stores/loading,js";
	import Loading from "./Loading.svelte";
$: $loading = !!$navigating
</script>
<Navbar/>
<Loading/>
<slot />