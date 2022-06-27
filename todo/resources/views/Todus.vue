<template>
<main>
    <h1>hello todo</h1>
</main>
</template>

<script>
import axios, { Axios } from "axios";
import { defineComponent, reactive, ref } from "vue";

export default defineComponent({
  setup() {
    const todos = reactive([]);
    const todoText = ref("");

    function addTodo() {
      todos.unshift({
        text: todoText.value,
        createAt: new Date(),
        done: false,
      });
    }
    function removeTodo(index) {
      if (!confirm("Are you sure?")) {
        return;
      }
      todos.splice(index, 1);
    }

    function getTodos() {
      axios.get("http://127.0.0.1:8000/api/todos").then((response) => {
        console.log(response);
      });
    }
    getTodos();
    return {
      todos,
      todoText,
      addTodo,
      markAsDone,
      markAsUndone,
      removeTodo,
    };
  },
});
</script>
