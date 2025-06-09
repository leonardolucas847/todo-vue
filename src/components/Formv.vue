<template>
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
</template>