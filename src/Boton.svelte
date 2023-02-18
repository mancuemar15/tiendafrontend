<script>
    import { onMount, getContext } from "svelte";
    import { jsonData } from "./store";

    export let tipo = "insertar";
    export let documento = {};

    const URL = getContext("URL");

    // let handler = () => {};

    function insertar() {
        const opciones = {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(documento),
        };
        fetch(URL.articulos, opciones)
            .then((res) => res.json())
            .then((data) => {
                jsonData.update((jsonData) => [...jsonData, data]);
                console.log(data);
            })
            .catch((error) => console.log(error));
    }

    function modificar() {
        const opciones = {
            method: "PUT",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(documento),
        };
        fetch(URL.articulos + `/${documento._id}`, opciones)
            .then((res) => res.json())
            .then((data) => console.log(data))
            .catch((error) => console.log(error));
    }

    function eliminar() {
        const opciones = {
            method: "DELETE",
        };
        fetch(URL.articulos + `/${documento._id}`, opciones)
            .then((res) => res.json())
            .then((data) => {
                jsonData.update((jsonData) =>
                    jsonData.filter(
                        (articulo) => articulo._id !== documento._id
                    )
                );
                console.log(data);
            })
            .catch((error) => console.log(error));
    }

    // function setup() {
    //     switch (tipo) {
    //         case "insertar":
    //             handler = insertar;
    //             break;
    //         case "modificar":
    //             handler = modificar;
    //             break;
    //         case "eliminar":
    //             handler = eliminar;
    //             break;
    //         default:
    //     }
    // }

    // onMount(setup);

    // function getHandler() {
    //     switch (tipo) {
    //         case "insertar":
    //             return insertar;
    //         case "modificar":
    //             return modificar;
    //         case "eliminar":
    //             return eliminar;
    //         default:
    //             return () => {};
    //     }
    // }

    // const handler = getHandler();

    // function getHandler()

    const handler = (() => {
        switch (tipo) {
            case "insertar":
                return insertar;
            case "modificar":
                return modificar;
            case "eliminar":
                return eliminar;
            default:
                return () => {};
        }
    })();
</script>

<input type="button" value={tipo.toUpperCase()} on:click={handler} />
