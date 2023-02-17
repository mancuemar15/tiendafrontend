<script>
    export let articulo= {
        nombre: '',
        precio: ''
    };
</script>

<input type="text" name="nombre" id="nombre" placeholder="Nombre" bind:value={articulo.nombre}>
<input type="number" name="precio" id="precio" placeholder="Precio" bind:value={articulo.precio}>
<slot />