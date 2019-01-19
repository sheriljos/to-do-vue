<template>
    <div>
        <div v-for="todo in todos" v-bind:key="todo.id">
            <TodoItem v-bind:todo="todo" v-on:deleteAnItem="deleteAnItem"/>
        </div>
    </div>
</template>

<script>
import TodoItem from './TodoItem';

export default {
    name: "Todos",
    components: {
        TodoItem
    },
    props: {
        todos : {
            type: Array,
            required: true,
        }
    },
    methods: {
        deleteAnItem(id) {            
            this.$emit('deleteAnItem', id)
        }
    }
}
</script>

<style scoped>

</style>