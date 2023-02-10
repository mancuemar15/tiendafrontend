<script>
    import {Link} from "svelte-routing";
</script>

<nav>
	<ul>
		<li><Link to="/">Inicio</Link></li>
		<li><Link to="/articulos">Artículos</Link></li>
		<li><Link to="/clientes">Clientes</Link></li>
	</ul>
</nav>

<style>
    nav {
        background-color: azure;
        padding: 10px;
    }

    ul {
        display: flex;
        justify-content: space-around;
        list-style-type: none;
    }
</style>