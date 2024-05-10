<script setup>
  const props = defineProps(["CadastraTarefa", "tarefaTemporaria",'trocarFiltro','editaTarefa']);
</script>
<template>
  <form @submit.prevent="props.CadastraTarefa" class="row">
    <div class="col">
      <input type="text" :value="props.tarefaTemporaria" @change="props.editaTarefa" placeholder="What you want to do today?"class="form-control" />
    </div>
    <div class="col-md-1">
      <button class="btn btn-primary">add task</button>
    </div>
    <select @change="props.trocarFiltro" class="form-control col">
      <option value="Todas tarefas">Todas tarefas</option>
      <option value="Finalizadas">Finalizadas</option>
      <option value="Pendentes">Pendentes</option>
    </select>
  </form>
</template>
