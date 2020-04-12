<template>
    <div>
        <form @submit="addTodo">
          <input type="text"  name="title" v-model="title" placeholder="Add Todos">
          <input type="submit" value="submit" class="btn">
        </form>
    </div>
</template>
<script>
//import { v4 as uuidv4 } from "uuid";
export default {
  name: "AddTodos",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        // id: uuidv4(),
        title: this.title,
        completed: false
      };
      //send up to parent
      console.log(newTodo);
      this.$emit("add-todo", newTodo);
      this.title = "";
    }
  }
};
</script>
<style scoped>
form {
  display: flex;
}
input[type="text"] {
  flex: 10;
}
input[type="submit"] {
  flex: 2;
}
</style>
