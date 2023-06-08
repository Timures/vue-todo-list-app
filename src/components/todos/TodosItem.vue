<template>
  <MyCheckbox :checked="todo.completed" :disabled="isDisabled">
    <div :class="todo.completed ? 'completed': ''">{{ todo.title }}</div>
  </MyCheckbox>
</template>

<script>
import MyCheckbox from '@/components/common/MyCheckbox'
export default {
  name: "todos-item",
  props: {
    todo: {
      type: Object,
      default: () => {},
    },
  },
  components: { MyCheckbox },
  data() {
    return {
      todoStatus: false,
    };
  },
  methods: {
    changeHandler(todo_id, completedValue) {
      console.log("change", completedValue);
      this.todoStatus = completedValue;

      fetch(`https://jsonplaceholder.typicode.com/todos/${todo_id}`, {
        method: "PATCH",
        body: JSON.stringify({
          completed: completedValue,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      })
        .then((response) => response.json())
        .then((json) => console.log(json));
    },
  },
};
</script>

<style>
.todos-item {
  display: flex;
  column-gap: 1rem;
  align-items: center;
  cursor: pointer;
}
.todos-checkbox {
  width: 0;
  height: 0;
}
.completed {
  text-decoration: line-through;
}
</style>
