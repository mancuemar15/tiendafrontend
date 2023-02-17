<script>
    import { onMount, getContext} from "svelte";

    export let tipo = 'insertar';
    export let documento = {};

    const URL = getContext("URL");

    let handler = () => {};

    function insertar() {
        let opciones = {
            method: 'POST',
            header: {"Content-Type": "application/json"},
            body: JSON.stringify(documento)
        }
        fetch(URL.articulos, opciones)
            .then(res => res.json())
            .then(data => console.log(data))
            .catch(error => console.log(error));
    }

    function modificar() {
        let opciones = {
            method: 'PUT',
            header: {"Content-Type": "application/json"},
            body: JSON.stringify(documento)
        }
        fetch(URL.articulos + `/${documento._id}`, opciones)
            .then(res => res.json())
            .then(data => console.log(data))
            .catch(error => console.log(error));
    }

    function eliminar() {
        let opciones = {
            method: 'DELETE'
        }
        fetch(URL.articulos + `/${documento._id}`, opciones)
            .then(res => res.json())
            .then(data => console.log(data))
            .catch(error => console.log(error));
    }

    function setup() {
        switch (tipo) {
            case 'insertar': handler = insertar;
                break;
            case 'modificar': handler = modificar;
                break;
            case 'eliminar': handler = eliminar;
                break;
            default:
        }
    }

    onMount(setup);
</script>

<input type="button" value={tipo.toUpperCase()} on:click={handler}>