<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue'; 
import ListaDeTarefas from './components/ListaDeTarefas.vue';


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
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"  />
     <Formulario :tarefa-temporaria="estado.tarefaTemporaria" :edita-tarefa-temporaria="evento => estado.tarefaTemporaria = evento.target.value" :cadastra-tarefa="CadastraTarefa" :trocar-filtro=" evento => estado.filtro = evento.target.value" /> 
     <ListaDeTarefas :tarefas="getTarefasFiltradas()" />


  </div>
</template>

<style scoped>

  .done{
    text-decoration: line-through;
  }

</style>
