<template>
  <div>
    <form @submit.prevent="addTodo">
      <input
        type="text"
        v-model="title"
        name="title"
        placeholder="add todo.."
      />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";

export default {
  name: "AddTodo",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    addTodo() {
      const newTodo = {
        id: uuidv4(),
        title: this.title,
        completed: false,
      };
      //send up to parent
      this.$emit("add-todo", newTodo);
      //newTodo'yu parametre olarak gönder
      this.title = "";
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
}
input[type="text"] {
  flex: 10;
  padding: 5px;
}
input[type="submit"] {
  flex: 2;
}
</style>
