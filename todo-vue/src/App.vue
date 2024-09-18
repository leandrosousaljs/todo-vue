<script setup>
import { reactive } from 'vue';
import Cabecalho from './Cabecalho.vue';
import Formulario from './Formulario.vue';
import Lista from './Lista.vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: []
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
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
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  }
</script>

<template>
  <div class="container">
    <Cabecalho  :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="e => estado.filtro = e.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    <Lista :tarefas="getTarefasFiltradas()" />
  </div>
</template>
