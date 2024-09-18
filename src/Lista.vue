<script setup>
    const props = defineProps(['tarefas'])
</script>

<template>
    <ul v-if="props.tarefas.length > 0" class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
    <p v-if="props.tarefas.every(t => t.finalizada) && props.tarefas.length > 0" class="mt-4 fs-5 text-center">
        Parabéns! Você completou todas as suas tarefas!🥳
    </p>
    <p v-else-if="props.tarefas.length === 0"class="mt-4 fs-5 text-center">
        Você não tem tarefas pendentes.
    </p>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }
</style>