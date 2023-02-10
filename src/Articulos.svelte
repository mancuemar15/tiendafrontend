<script>
    import {onMount} from "svelte";
    import Buscar from "./Buscar.svelte";

    let data = [];
    let patron = "Camisa";

    const getArticulos = async() => {
        const response = await fetch('https://tiendabackend.fly.dev/api/articulos/');
        data = await response.json();

    } 

    onMount(getArticulos);

    $: articulosFiltrados = data.filter( articulo => RegExp(patron, "i").test(articulo.nombre));

</script>

<h1>Artículos</h1>

<Buscar bind:busqueda={patron}/>
<!-- <Buscar bind:busqueda/> -->

<hr>

{#each articulosFiltrados as articulo}
    {articulo.nombre}<br>
    {articulo.precio}<hr>
{/each}

<style>
    h1 {
        text-align: center;
    }
</style>