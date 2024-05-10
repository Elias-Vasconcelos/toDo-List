<script setup>
  import { reactive } from "vue";
  import Cabecalho from "./components/Cabecalho.vue";
  import Formulario from "./components/Formulario.vue";
  import Lista from "./components/Lista.vue";

  const estado = reactive({
    tarefaTemporaria: "",
    filtro: "todas as taferas",
    tarefa: [
      {
        titulo: "estudar react",
        finalizada: false,
      },
      {
        titulo: "estudar vueJs",
        finalizada: false,
      },
      {
        titulo: "ir para a academios",
        finalizada: true,
      },
    ],
  });
  const GetTarefasPendentes = () => {
    return estado.tarefa.filter((tarefa) => !tarefa.finalizada);
  };
  const GetTarefasFinalizadas = () => {
    return estado.tarefa.filter((tarefa) => tarefa.finalizada);
  };
  const GetTarefasFilt4radas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case "Finalizadas":
        return GetTarefasFinalizadas();
      case "Pendentes":
        return GetTarefasPendentes();
      default:
        return estado.tarefa;
    }
  };
  const CadastraTarefa = ()=>{
    const NovaTarefa = {
      titulo: estado.tarefaTemporaria,
      finalizada: false,
    }
    estado.tarefa.push(NovaTarefa);
    estado.tarefaTemporaria = "";
  }
</script>

<template>
  <div class="container">
    <Cabecalho :tarefa-pendentes="GetTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento =>  estado.filtro = evento.target.value" :tarefa-temporaria="estado.tarefaTemporaria" :edita-tarefa ="evento => estado.tarefaTemporaria = evento.target.value" :cadastra-tarefa="CadastraTarefa()" />
    <Lista :tarefas="GetTarefasFilt4radas()" />
  </div>
</template>
<style scoped>
  .Done {
    text-decoration: line-through;
  }
</style>
