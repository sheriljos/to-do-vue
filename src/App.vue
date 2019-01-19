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
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Todos,
    Header,
    AddTodo
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteAnItem(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(response => {
          const result = this.todos.filter(todo => todo.id != id);      
          this.todos = result;
        })
    },
    AddNewTodo(newTodo) {
      const newValue = {
        title: newTodo.title,
        completed: newTodo.completed
      }
      axios.post('https://jsonplaceholder.typicode.com/todos?_limit=5', newValue)
        .then(response => 
          this.todos = [...this.todos, newValue])
        .catch(err => 
          console.warn('error', err))
    },
  },
  created() {
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
        .then(response => 
          this.todos = response.data)
        .catch(err => {
          console.warn('error', err)})
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
