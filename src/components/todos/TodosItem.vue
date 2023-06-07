<template>
     <label :class="{ completed: todo.completed || todoStatus }">
          <input type="checkbox" v-model="todoStatus" @change="changeHandler(todo.id,todoStatus)">
          {{ todo.title }}
        </label>
</template>

<script>
export default {
    name: 'todos-item',
    props: {
        todo: {
            type: Object,
            default: ()=>{}
        }
    },
    data(){
        return {
            todoStatus: false,
        }
    },
    methods: {
        changeHandler(todo_id, completedValue){
            console.log('change', completedValue);

            fetch(`https://jsonplaceholder.typicode.com/todos/${todo_id}`, {
  method: 'PATCH',
  body: JSON.stringify({
    completed: completedValue,
  }),
  headers: {
    'Content-type': 'application/json; charset=UTF-8',
  },
})
  .then((response) => response.json())
  .then((json) => console.log(json));
            
        }
    }
}
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>