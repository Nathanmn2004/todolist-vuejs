<script setup>
import { reactive } from 'vue';


  const estado = reactive({
    filtro: 'todas',

    tarefaTemporaria: '',
    tarefas: [{
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar SAAS',
      finalizada: false,
    },
    {
      titulo:'Ir para Academia',
      finalizada:true,
    }
  ],
  })

  const getTarefasPendentes = () => {
     return estado.tarefas.filter(tarefa => tarefa.finalizada == false);
  }

  const getTarefasFinalizadas = () => {
     return estado.tarefas.filter(tarefa => tarefa.finalizada == true);
  }

  function getTarefasFiltradas(){
    const {filtro} = estado;


    switch(filtro){
      case 'Tarefas Pendentes':
        return getTarefasPendentes();

      case 'Tarefas Finalizadas':
        return getTarefasFinalizadas();

      default:
        return estado.tarefas;
    }

  }

  const CadastraTarefa = () => {
    
    
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
    <header class="p-4 mb-3 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p> Você Possui {{ getTarefasPendentes().length }} Tarefas Pendentes</p>

    </header>

    <div class="container">
      <form action="" @submit.prevent="CadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemporaria"  @change="evento => estado.tarefaTemporaria = evento.target.value" type="text" placeholder="Digite a descrição da tarefa!" class="form-control" required>
        </div>
        <div class="col md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>

        <div class="col md-2">
          <select class="form-control" @change="evento => estado.filtro = evento.target.value">
            <option value="Todas as tarefas">Todas Tarefas</option>
            <option value="Tarefas Pendentes">Tarefas Pendentes</option>
            <option value="Tarefas Finalizadas">Tarefas Finalizadas</option>
          </select>
        </div>

      

      </div>
    </form>

    
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox" @change="evento => tarefa.finalizada = evento.target.checked">
        <label :for="tarefa.titulo" class="ms-3"  :class="{ done: tarefa.finalizada == true }"> {{ tarefa.titulo }}</label>
      </li>
    </ul>




    </div>

  </div>
</template>

<style scoped>

  .done{
    text-decoration: line-through;
  }

</style>
