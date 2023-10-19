<script setup>
const props = defineProps(['tarefas', 'tarefasPendentes']);
</script>


<template>
    <ul v-if="props.tarefas.length == 0" class="list-unstyled">
        <li>
            <h3 class="mt-5">Não há tarefas cadastradas</h3>
        </li>
    </ul>
    <ul v-else-if="props.tarefas.length > 0" class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>