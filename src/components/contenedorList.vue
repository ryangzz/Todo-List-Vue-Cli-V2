<template>
    <div>
        <section class="main">
            <input id="toggle-all" class="toggle-all" type="checkbox" @click="completarAll" v-model="marcar">
            <label for="toggle-all">Mark all as complete</label>
            <ul class="todo-list" v-for="(elem) of lista" :key="elem.id">
                <li :class="{'completed':elem.estatus, 'pendiente':!elem.estatus}" :data-id="elem.id" v-if="elem.visible">
                    <div class="view">
                        <input class="toggle" type="checkbox" :checked="elem.estatus" v-model="elem.estatus" @click="completarTarea(elem.id, elem.estatus)">
                        <label>{{elem.tarea}}</label>
                        <button class="destroy" @click="del(elem.id)"></button>
                    </div>
                    <input class="edit" value="Create a TodoMVC template">
                </li>
            </ul>
        </section>  
    </div>
</template>
<script>
export default {
    data() {
        return {
            marcar:false
        }
    },
    props:{
        lista:Object
    },
    methods: {
        del(vid){
            this.$emit('delTarea', vid);
        },
        completarAll(){
            this.$emit('completeAll', !this.marcar)
        },
        completarTarea(id, estatus){
            this.$emit('completeTarea', id, !estatus);
        }
    },
}
</script>
<style>
    
</style>