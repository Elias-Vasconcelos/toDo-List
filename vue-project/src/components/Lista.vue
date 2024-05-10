<script setup >
    const props = defineProps(['tarefas']);
</script>
<template>
    <ul class="list-group mt-4">
        <li class="list-group-item p-3" v-for="tarefa in props.tarefas ">
            <input @change="(envento) => (tarefa.finalizada = envento.target.checked)" :checked="tarefa.finalizada" type="checkbox" :id="tarefa.titulo" />
            <label :for="tarefa.titulo" :class="{ Done: tarefa.finalizada }" class="ms-3">{{tarefa.titulo}}</label>
        </li>
    </ul>
</template>
