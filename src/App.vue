<template>
  <div id="app">
    <Header />
    <Todos v-bind:todos="todos"
           v-on:deleteAnItem="deleteAnItem"
    />
    <AddTodo v-on:add-todo="AddNewTodo"/>
  </div>
</template>

<script>
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';
import Header from './components/layouts/Header'

export default {
  name: 'app',
  components: {
    Todos,
    Header,
    AddTodo
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Complete the Todo App",
          completed: false
        },
        {
          id: 2,
          title: "Complete the vue-super-form",
          completed: false
        },
        {
          id: 3,
          title: "Do washing",
          completed: true
        }
      ]
    }
  },
  methods: {
    deleteAnItem(id) {
      const result = this.todos.filter(todo => todo.id != id);
    },
    AddNewTodo(newTodo) {      
      this.todos = [...this.todos, newTodo];
    }
  }
}
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
</style>
