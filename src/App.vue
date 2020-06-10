<template>
  <div id="app">
    <Todos />
  </div>
</template>

<script>
import Todos from "./components/Todos";

export default {
  name: "App",
  components: {
    Todos
    //kullanılan komponentler
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "todo one",
          completed: false
        },
        {
          id: 2,
          title: "todo two",
          completed: true
        },
        {
          id: 3,
          title: "todo three",
          completed: false
        }
      ]
    };
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
}
</style>
