
<script setup>

  const props = defineProps(['cadastraTarefa' , 'tarefaTemporaria' , 'trocarFiltro', 'editaTarefaTemporaria'])

</script>




<template>

    

    <form action="" @submit.prevent="props.cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="props.tarefaTemporaria"  @change="props.editaTarefaTemporaria" type="text" placeholder="Digite a descrição da tarefa!" class="form-control" required>
        </div>
        <div class="col md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>

        <div class="col md-2">
          <select class="form-control" @change="props.trocarFiltro">
            <option value="Todas as tarefas">Todas Tarefas</option>
            <option value="Tarefas Pendentes">Tarefas Pendentes</option>
            <option value="Tarefas Finalizadas">Tarefas Finalizadas</option>
          </select>
        </div>

      

      </div>
    </form>
</template>