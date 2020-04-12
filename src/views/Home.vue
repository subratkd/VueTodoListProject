<template>
  <div id="app">
    <AddTodos  v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodos from "../components/AddTodos";
import axios from "axios";
export default {
  name: "Home",
  components: {
    Todos,
    AddTodos
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id != id);
      // axios
      //   .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      //spread operator
      // .then(res => (this.todos = this.todos.filter(todo => todo.id !== id)))
      // .error(error => console.log("error ===>" + error));
      //this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo) {
      //this.todos = [...this.todos, newTodo];
      const { title, completed } = newTodo;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed
        })
        //spread operator
        .then(response => (this.todos = [...this.todos, response.data]))
        .error(error => console.log("error ===>" + error));
    }
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(response => (this.todos = response.data))
      .catch(error => console.log(error));
  }
};
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
