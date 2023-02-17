<script>
    import { getContext, onMount} from "svelte";
    import { jsonData } from "./store.js";
    import Buscar from "./Buscar.svelte";
    import Articulo from "./Articulo.svelte";
    import Boton from "./Boton.svelte";

    let articuloInsertar = {};
    let articulosFiltrados = [];
    let patron = "";
    const URL = getContext("URL");

    const getArticulos = async() => {
        const response = await fetch(URL.articulos);
        $jsonData = await response.json();
    } 

    onMount(getArticulos);

    $: articulosFiltrados = $jsonData.filter( articulo => RegExp(patron, "i").test(articulo.nombre));

</script>

<h1>Artículos</h1>

<Buscar bind:busqueda={patron}/>
<!-- <Buscar bind:busqueda/> -->

<hr>

<Articulo bind:articulo={articuloInsertar}>
    <Boton tipo="insertar" documento={articuloInsertar}/> 
</Articulo>
<br>

{#each articulosFiltrados as articulo}
    <Articulo {articulo}>
        <Boton tipo="modificar" documento={articulo}/> 
        <Boton tipo="eliminar" documento={articulo}/> 
    </Articulo>
    <br>
{/each}

<style>
    h1 {
        text-align: center;
    }
</style>