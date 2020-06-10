<template>
  <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
    <!-- : is condition -->
    <p>
      <input type="checkbox" v-on:change="markComplete" />
      <!--change event then call markComplete method-->
      {{todo.title}}
      <button @click="$emit('del-todo',todo)" class="del">x</button>
      <!-- v-bind yerine @click kullanabiliriz, parametre olarak todo gönder, yukarı componente emit et-->
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem", //component name
  props: ["todo"], //Todos.vue'dan gelen todo prop
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    }
  }
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}
.is-complete {
  text-decoration: line-through;
}
.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>