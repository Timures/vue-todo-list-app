<template>
    <div class="todos-list">
      <ul>
        <li v-for="todo in todos" :key="todo.id">
          <TodosItem :todo="todo" />
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  import TodosItem from "@/components/todos/TodosItem";
  export default {
    name: "payments-list",
    props: {
      todos: {
        type: Array,
        default: () => {
          [];
        },
      },
    },
    components: { TodosItem },
  };
  </script>
  