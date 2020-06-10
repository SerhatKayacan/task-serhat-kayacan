<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in todos">
      <!--looping todos prop-->
      <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo',todo)" />
      <!--pass in todo-->
      <!--yakala, tekrar bir yukarı emit ediyoruz-->
    </div>
  </div>
</template>

<script>
import TodoItem from "./Todoitem.vue";

export default {
  name: "Todos", //component name
  components: {
    TodoItem
  },
  props: ["todos"] // App.vue'dan geliyo
};
</script>

<style scoped>
</style>