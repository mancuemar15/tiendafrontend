<script>
    export let articulo = {
        nombre: '',
        precio: 0,
    };
</script>

<input
    type="text"
    name="nombre"
    placeholder="Nombre"
    bind:value={articulo.nombre}
/>
<input
    type="number"
    name="precio"
    placeholder="Precio"
    min="0"
    step="0.01"
    bind:value={articulo.precio}
/>
<slot />
