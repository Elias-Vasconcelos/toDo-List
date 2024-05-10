<script setup>
const props = defineProps(["tarefaPendentes"]);
</script>

<template>
  <header class="p-5 mb-4 mt-4 bg-light rounded-6">
    <h1>Minhas Tarefas</h1>
    <p>voce tem {{ props.tarefaPendentes }} tarefas pendentes!</p>
  </header>
</template>
