<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    tarefaTemporaria: '',
    filtro: 'todas as taferas',
      tarefa: [
      {
        titulo: 'estudar react',
        finalizada: false,
      },
      {
        titulo: 'estudar vueJs',
        finalizada: false,
      },
      {
        titulo: 'ir para a academios',
        finalizada: true,
      }
      ]
  })
  const GetTarefasPendentes = () => {
    return estado.tarefa.filter(tarefa => !tarefa.finalizada )
  }
  const GetTarefasFinalizadas = () => {
    return estado.tarefa.filter(tarefa => tarefa.finalizada )
  }
  const GetTarefasFilt4radas = () =>{
    const {filtro} =  estado;

    switch(filtro){
      case'Finalizadas':
      return GetTarefasFinalizadas();
      case 'Pendentes':
      return GetTarefasPendentes();
      default:
        return estado.tarefa
    }
  }
  const CadastraTarefa = () =>{
      const NovaTarefa = {
        titulo: estado.tarefaTemporaria,
        finalizada: false,
      }
      estado.tarefa.push(NovaTarefa);
      estado.tarefaTemporaria = '';
    }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-6" >
      <h1>Minhas Tarefas</h1>
      <p>voce tem {{ GetTarefasPendentes().length }} tarefas pendentes!</p>
    </header>
    <form  @submit.prevent="CadastraTarefa" class="row">
      <div class="col">
        <input type="text"  :value="estado.tarefaTemporaria"  @change="evento => estado.tarefaTemporaria = evento.target.value " placeholder="What you want to do today?" class="form-control">
      </div>
      <div class="col-md-1"><button class="btn btn-primary">add task</button></div>
      <select  @change="evento => estado.filtro = evento.target.value" class="form-control col">
        <option value="Todas tarefas">Todas tarefas</option>
        <option value="Finalizadas">Finalizadas</option>
        <option value="Pendentes">Pendentes</option>
      </select>
    </form  >
    <ul class="list-group mt-4">
      <li class="list-group-item p-3 " v-for="tarefa in GetTarefasFilt4radas()" >
        <input @change="envento => tarefa.finalizada = envento.target.checked "  :checked="tarefa.finalizada"   type="checkbox" :id="tarefa.titulo">
        <label :for="tarefa.titulo" :class="{Done: tarefa.finalizada}"  class="ms-3">{{ tarefa.titulo }}</label>
      </li>
    </ul>
  </div>

</template>
<style scoped>  

.Done { 
  text-decoration: line-through;
}

</style>
