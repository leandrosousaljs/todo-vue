<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas tarefas</h1>
        <p v-if="props.tarefasPendentes == 0">Adicione novas tarefas abaixo:</p>
        <p v-else>
            Você possui {{ props.tarefasPendentes }} tarefa(s) pendentes.
        </p>
    </header>
</template>