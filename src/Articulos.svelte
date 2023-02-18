<script>
    import { onMount, getContext } from "svelte";
    import { jsonData } from "./store.js";
    import Buscar from "./Buscar.svelte";
    import Articulo from "./Articulo.svelte";
    import Boton from "./Boton.svelte";

    const URL = getContext("URL");

    let articulo = {};
    let articulosFiltrados = [];
    let busqueda = "";

    const getArticulos = async () => {
        const response = await fetch(URL.articulos);
        $jsonData = await response.json();
    };

    onMount(getArticulos);

    $: articulosFiltrados = $jsonData.filter((articulo) =>
        RegExp(busqueda, "i").test(articulo.nombre)
    );
</script>

<h1>Artículos</h1>

<Buscar bind:busqueda />
<hr />

<Articulo {articulo}>
    <Boton tipo="insertar" documento={articulo} />
</Articulo>
<br />

{#each articulosFiltrados as articulo}
    <Articulo {articulo}>
        <Boton tipo="modificar" documento={articulo} />
        <Boton tipo="eliminar" documento={articulo} />
    </Articulo>
    <br />
{/each}

<style>
    h1 {
        text-align: center;
    }
</style>
