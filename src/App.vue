<script setup>
  import { reactive } from 'vue';
  import Headerv from './components/Headerv.vue';
  import Formv from './components/Formv.vue';
  import ListTasks from './components/ListTasks.vue';
  const estado = reactive({
    filtro : 'Todas',
    tarefaTemporaria: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false
      },
      {
        titulo: 'estudar SASS',
        finalizada: false,
      },
      {
        titulo: 'is para a academia',
        finalizada: true,
      },
    ]
  })
  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
  }
  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
  }
  const getTarefasFriltradas = () => {
    const filtro = estado.filtro
    switch (filtro) {
      case 'pendentes': 
      return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
        default :
        return estado.tarefas;  
      }
  }
  const cadastraTarefa = () => {
    const novaTarefa = {
      titulo: estado.tarefaTemporaria,
      finalizada: false,
    }
    estado.tarefas.push(novaTarefa);
    estado.tarefaTemporaria = '';
  }
</script>

<template>
  <div class="container">
    <Headerv />
    <Formv />
    <ListTasks />
    

  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
