<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
    <!--datadaki todos props olarak geçiyo-->
    <!--v-on:del-todo ile eventi yakala-->
    <div v-if="filtervalue === 'not filter'">
      <ul v-bind:key="todo.id" v-for="todo in filtered">
        <li>{{ todo.title }}</li>
      </ul>
    </div>
    <div>
      <button class="filter" v-on:click="filter()">{{ filtervalue }}</button>
      <button class="logout" v-on:click="logout()">logout</button>
    </div>
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";
import axios from "axios";

export default {
  name: "Secure",
  components: {
    Header,
    Todos,
    AddTodo,
    //kullanılan komponentler
  },
  data() {
    return {
      todos: [],
      filtervalue: "filter",
      filtered: [],
    };
  },
  methods: {
    logout() {
      this.$store.commit("setAuthentication", false);
      this.$router.replace({ name: "login" });
    },
    filter() {
      if (this.filtervalue === "filter") {
        this.filtered = this.todos.filter((todo) => {
          return todo.completed === true;
        });
        this.filtervalue = "not filter";
      } else {
        this.filtervalue = "filter";
      }
    },
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    addTodo(newTodo) {
      this.todos.push(newTodo);
    },
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((res) => (this.todos = res.data))
      .catch((err) => console.log(err));
  },
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
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
.logout {
  float: right;
  width: 100px;
  height: 40px;
}
.filter {
  width: 100px;
  height: 40px;
}
</style>
