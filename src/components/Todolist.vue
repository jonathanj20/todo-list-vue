<template>
    <div>
        <h2>Tareas Vue.js</h2>
        <input type="text" placeholder="Escribe una tarea por hacer" v-model="tarea.texto">
        <button @click="agregarTarea">Agregar tarea</button>
        <table>
            <tr>
                <td><b>Hecho!</b></td>
                <td><b>Tarea</b></td>
                <td><b>Eliminar</b></td>
                <td><b>Editar</b></td>
            </tr>
            <tr v-for="(task, index) in tareas" :key="index">
                <td><input type="checkbox" @click="cambiarEstado(task)"></td>
                <td :class="{ completado: task.estaCompletado }" :contenteditable="task.esEditable">{{ task.texto }}</td>
                <td><button @click="eliminarTarea(index)">Eliminar</button></td>
                <td><button @click="editarTarea(task)">Editar</button></td>
            </tr>
        </table>
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
.completado {
    text-decoration: line-through;
}
</style>
