<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png">
      <section class="todoapp">
        <headerList :titulo="titulo" @addTarea="addTarea" ></headerList>
        <contenedorList :lista="lista" @delTarea="delTarea" @completeAll="completeAll" @completeTarea="completeTarea"></contenedorList>
        <footerList @delCompleted="delCompleted" @filters="filters" :pendientes="numPendientes"></footerList>
      </section>
      <footerInfo></footerInfo>
  </div>
</template>

<script>
import headerList from './components/header'
import contenedorList from './components/contenedorList'
import footerList from './components/footerList'
import footerInfo from './components/footer.vue'

export default {
  name: 'App',
  components: {
    headerList,
    contenedorList,
    footerList,
    footerInfo
  },
  mounted() {
    this.lista = (localStorage.getItem('tareas')) ? JSON.parse(localStorage.getItem('tareas')) : [];
  },
  data() {
    return {
      titulo:"Todo List V2 Con Vue Cli",
      lista:[],
    }
  },
  methods: {
    addTarea(tarea){
      let id = 't'+this.lista.length+1;
      this.lista.push({tarea, estatus:false, id, visible:true});
      this.saveLocalStorage();
    },
    delTarea(id){
      let index = this.lista.findIndex(el => el.id===id);
      this.lista.splice( index, 1 );
      this.saveLocalStorage();
    },
    completeAll(marcar){
      this.lista.forEach((el, index) => { (marcar) ? this.lista[index].estatus=true : this.lista[index].estatus=false;  });
      this.saveLocalStorage();
    },
    delCompleted(){
      this.lista = this.lista.filter(el => !el.estatus);
      this.saveLocalStorage();
    },
    completeTarea(id, value){
      let index = this.lista.findIndex(el=> el.id===id);
      this.lista[index].estatus = value;
      this.saveLocalStorage();
    },
    filters(val){
      (val==1) ? this.lista.forEach((el, index) => (el.estatus) ? this.lista[index].visible=false : this.lista[index].visible=true)
              : (val==2) ?  this.lista.forEach((el, index) => (el.estatus) ? this.lista[index].visible=true : this.lista[index].visible=false)
              :  this.lista.forEach((el, index) =>this.lista[index].visible=true);
    },
    saveLocalStorage(){
      localStorage.setItem('tareas', JSON.stringify(this.lista));
    },
  },
  computed: {
    numPendientes(){
      let pendientes = 0;
      this.lista.forEach(el => (!el.estatus) ? pendientes+=1 : pendientes+=0);
      return pendientes*1;
    }
  },
}
</script>

<style>
@import 'style.css';
</style>
