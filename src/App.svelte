<script>
	import { setContext } from "svelte";
	import Nav from "./Nav.svelte";
	import Contenido from "./Contenido.svelte";
	import {Router} from "svelte-routing";

	const URL = {
		articulos: "https://tiendabackend.fly.dev/api/articulos",
		clientes: "https://tiendabackend.fly.dev/api/clientes"
	};
	setContext("URL", URL);
</script>

<Router>
	<Nav />
	<Contenido />
</Router>


<style>
	:global(body) {
		margin: 0;
		padding: 0;
		color: tomato;
		background-color: darkblue;
	}
</style>