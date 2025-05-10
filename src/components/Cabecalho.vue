
<script setup>

    const props = defineProps(['tarefasPendentes'])

</script>



<template>
    <header class="p-4 mb-3 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p> Você Possui {{ props.tarefasPendentes }} Tarefas Pendentes</p>

    </header>

</template>