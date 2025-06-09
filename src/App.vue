<script setup>
  import { reactive } from 'vue';
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
    <header class="p-5 mb-4 mt-4 mb-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa()">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemporaria" type="text" @change="evento => estado.tarefaTemporaria = evento.target.value" required placeholder="Digite a descrição da tarefa" class="form-crontrol">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="Todas">Todas Tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFriltradas()">
        <input  @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
