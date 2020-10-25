<template>
    <div>
        <header class="header">
            <h1>{{titulo}}</h1>
            <input  type="text" class="new-todo" placeholder="¿Qué necesita ser hecho?" autofocus  @keyup.enter.prevent="agregarTarea" v-model="tarea">
        </header>  
    </div>
</template>

<script>
export default {
    data() {
        return {
            tarea:''
        }
    },
    props:{
        titulo:String
    },
    methods: {
        agregarTarea(){
            if(this.tarea=='') return;
            this.$emit('addTarea', this.tarea);
            this.tarea = '';
        }
    },
}
</script>

<style>

</style>