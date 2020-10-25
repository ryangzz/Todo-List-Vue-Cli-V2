<template>
    <footer class="footer">
        <span class="todo-count"><strong>{{pendientes}}</strong> pendiente(s)</span>
        <ul class="filters">
            <li>
                <a class="selected filtro" @click="filterTareas(0)">Todos</a>
            </li>
            <li>
                <a class="filtro" @click="filterTareas(1)">Pendientes</a>
            </li>
            <li>
                <a class="filtro" @click="filterTareas(2)">Completados</a>
            </li>
        </ul>
        <button class="clear-completed" type="button" @click="eliminarCompletados">Borrar completados</button>
    </footer>
</template>

<script>
export default {
    props:{
        pendientes:Number
    },
    mounted() {
        this.addClass();
    },
    methods: {
        eliminarCompletados(){
            this.$emit('delCompleted');
        },
        addClass(){
            let filtro = document.querySelectorAll(".filtro");
            filtro.forEach(el => {
                el.addEventListener('click', function(){
                    document.querySelector(".selected").classList.remove("selected");
                    this.classList.add("selected");
                })
            });
        },
        filterTareas(val){
            this.$emit('filters', val)
        }
    },
}
</script>

<style>

</style>