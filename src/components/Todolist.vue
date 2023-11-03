<template>
    <div class="contenedor">
        <section class="encabezado">
            <h2 class="titulo">Tareas Vue.js</h2>
            <input type="text"  class="input" placeholder="Escribe una tarea por hacer" v-model="tarea.texto">
            <button class="btnAgregar" @click="agregarTarea()">+</button>
        </section>
        <section class="tabla">
            <table>
                <tr class="fila">
                    <td><b>Hecho!</b></td>
                    <td><b>Tarea</b></td>
                    <td><b>Eliminar</b></td>
                    <td><b>Editar</b></td>
                </tr>
                <tr v-for="(task, index) in tareas" :key="index" class="fila">
                    <td class="columna__checkbox"><input type="checkbox" @click="cambiarEstado(task)"></td>
                    <td :class="{ completado: task.estaCompletado }" :contenteditable="task.esEditable">{{ task.texto }}</td>
                    <td><button @click="eliminarTarea(index)" class="btnEliminar">Eliminar</button></td>
                    <td><button @click="editarTarea(task)" class="btnEditar">Editar</button></td>
                </tr>
            </table>
        </section>
    </div>
</template>

<script>
import { ref } from 'vue';

export default {
    setup() {
        const tareas = ref([]);

        const tarea = ref({
            texto: '',
            estaCompletado: false,
            esEditable: false
        });

        /*Se agrega una copia del objeto, a un objeto nuevo antes de agregarlo al array de tareas.
        Para evitar que todos los objetos tengan la misma referencia, y cada objeto sea independiente*/ 
        function agregarTarea() {
            tareas.value.push({...tarea.value}); 
            tarea.value.texto = '';
        }

        const cambiarEstado = (task) => task.estaCompletado = !task.estaCompletado;
        const eliminarTarea = (index) => tareas.value.splice(index, 1);
        const editarTarea = (task) => task.esEditable = !task.esEditable;

        return { tarea, tareas, agregarTarea, cambiarEstado, eliminarTarea, editarTarea };
    }
}
</script>

<style scoped>
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.completado {
    text-decoration: line-through;
}

/**Estilos para la tabla y el contenedor*/
.contenedor{
    background-color: #1b2328;
    width: 100%;
    min-height: 100vh;
    color: white;
    display: flex;
    align-items: center;
    flex-direction: column;
    font-family: Arial, Helvetica, sans-serif;
    padding: 1em;
    transition: all 1s ease;
}

.tabla{
    background-color: #343c40;
    color: #fff;
    margin-top: 1em;
}

table{
    border-collapse: collapse;
}

.encabezado{
    text-align: center;
}
.titulo{
    text-align: center;
    font-size: 2em;
    letter-spacing: 5px;
    margin-bottom: .5em;
}

.btnAgregar{
    padding:.3em 1em;
    cursor: pointer;
    color: #fff;
    font-weight: 800;
    background-color: #000;
    border: 2px solid #fff;
    font-size: 1em;
    margin-left: 1em;
}

.btnAgregar:hover{
    background-color: #8c8a8a;
}

.input{
    border: none;
    border-bottom: 3px solid #fff;
    background: none;
    width: 15em;
    color: #fff;
    outline: none;
}

input::placeholder{
    color: #dce5e9;
}

td{
    padding: 1em;
    width: 8em;
}

tr{
    transition: all .5s ease;
}

tr:hover{
    background-color: #464646;
}

.columna__checkbox{
    text-align: center;
}

.btnEliminar, .btnEditar{
    padding: .5em 1em;
    cursor: pointer;
}

.btnEditar{
    background-color: #fff;
    border: none;
}

.btnEditar:hover{
    background-color: #f1f0f0;
}

.btnEliminar{
    background-color: #e81818;
    color: #fff;
    border: 1px solid #e81818;
    font-weight: bold;
    cursor: pointer;
}

.btnEliminar:hover{
    background-color: #e85454;
}
</style>
