<template>
  <div class="todos-list">
    <ul>
      <li
        v-for="todo in todos"
        :key="todo.id"
      >
        <TodosItem :todo="todo" />
      </li>
    </ul>
  </div>
</template>

<script>
import TodosItem from "@/components/todos/TodosItem";
export default {
  name: "PaymentsList",
  components: { TodosItem },
  props: {
    todos: {
      type: Array,
      default: () => {
        [];
      },
    },
  },
};
</script>

<style lang="scss" scoped>
.todos-list {
  ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow: auto;
  }
}
</style>
