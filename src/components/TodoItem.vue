<template>
    <div class="todo-item" v-bind:class="classFinder">
        <input type="checkbox" v-on:input="toggleStatus">
        <p>{{todo.title}}</p>
        <button class="del" @click="deleteItem">x</button>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    props: {
        todo: {
            type: Object,
            required: true
        }
    },
    computed: {
        classFinder() {
            return this.todo.completed &&
            "is-complete";
        }
    },
    methods: {
        toggleStatus() {
            this.todo.completed = !this.todo.completed;
        },
        deleteItem() {
            this.$emit('deleteAnItem', this.todo.id)
        }
    }
}
</script>

<style scoped>
    .todo-item {
        display: flex;
        background: rgb(236, 198, 198);
        padding: 10px;
        border-bottom: 1px grey dotted;
    }

    .is-complete {
        text-decoration: line-through;
    }

    .del {
        background: red;
        width: 20px;
        height: 20px;
    }
</style>