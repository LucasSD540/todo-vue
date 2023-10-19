<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: []
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada);
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada);
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {
    let tarefaDupla = false;
    
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false
    }

    for (let i = 0; i < estado.tarefas.length; i++) {
      if (tarefaNova.titulo === estado.tarefas[i].titulo) {
        tarefaDupla = true;
        break;
      }
    }

    if (tarefaDupla) {
      alert("Essa tarefa já foi cadastrada");
    } else {
      estado.tarefas.push(tarefaNova);
      estado.tarefaTemp = '';
    }
  }
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    <ListaDeTarefas :tarefas-pendentes="getTarefasPendentes().length" :tarefas="getTarefasFiltradas()" />

  </div>
</template>