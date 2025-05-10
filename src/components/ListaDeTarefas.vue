
<script setup>


  const props = defineProps(['tarefas']);

</script>



<template>


<ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in props.tarefas">
        <input :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox" @change="evento => tarefa.finalizada = evento.target.checked">
        <label :for="tarefa.titulo" class="ms-3"  :class="{ done: tarefa.finalizada == true }"> {{ tarefa.titulo }}</label>
      </li>
    </ul>
</template>