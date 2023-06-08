<template>
  <div class="user-item">
    {{ user.name }}
    <button @click="showModalUserTodos(user.id)">Задачи</button>
    <button @click="showModalUserEdit(user.id)">Редактировать</button>
  </div>

  <Modal :visible="isModalTodosVisible" @close="closeModal">
    <template v-slot:header>
      <h3>Задачи пользователя</h3>
    </template>
    <template v-slot:body>
      <TodosList :todos="userTodos"/>
    </template>
    <template v-slot:footer>
      <button @click="closeModal">Закрыть</button>
    </template>
  </Modal>

  <Modal :visible="isModalVisible" @close="closeModal">
    <template v-slot:header>
      <h3>Редактировать пользователя</h3>
    </template>
    <template v-slot:body>
      {{ user.id }}
      <form action="">
        <input type="text" name="name" id="userName" v-model="userData.name">
        <input type="text" name="phone" id="userPhone" v-model="userData.phone">
        <input type="text" name="email" id="userEmail" v-model="userData.email">
      </form>
      <button @click="updateUser(user.id)">Сохранить</button>
    </template>
    <template v-slot:footer>
      <button @click="closeModal">Закрыть</button>
    </template>
  </Modal>

</template>

<script>
import Modal from "@/components/common/MyModal";
import TodosList from "@/components/todos/TodosList.vue";
export default {
  name: "user-item",
  props: {
    user: {
      type: Object,
      default: () => {},
    },
  },
  components: {
    Modal,
    TodosList
  },
  data() {
    return {
      isModalVisible: false,
      isModalTodosVisible: false,
      userTodos: [],
      userData: {
        name: '',
        phone: '',
        email: ''
      }
    };
  },
  emits:['update'],
  methods: {
    updateUser(user_id){
      this.$emit('update', user_id, this.userData)
      console.log('user update ', user_id);
      this.isModalVisible = false
    },
    showModalUserTodos(user_id){
        // console.log('todos',user_id, `https://jsonplaceholder.typicode.com/user/${user_id}/todos?limit=10`)
        this.isModalTodosVisible = true
        fetch(`https://jsonplaceholder.typicode.com/user/${user_id}/todos?_limit=10`)
        .then(response => response.json())
        .then(data => {
          this.userTodos = data; // Получаем только первые 10 пользователей
        })
        .catch(error => {
          console.error('Ошибка при получении пользователей:', error);
        });
    },
    showModalUserEdit(user_id) {
      this.isModalVisible = true;
      fetch(`https://jsonplaceholder.typicode.com/users/${user_id}`)
        .then(response => response.json())
        .then(data => {
          this.userData.name = data.name; 
          this.userData.phone = data.phone;
          this.userData.email = data.email;
        })
        .catch(error => {
          console.error('Ошибка при получении пользователей:', error);
        });
      console.log('user name ', user_id);
    },
    closeModal() {
      this.isModalVisible = false;
      this.isModalTodosVisible = false;
    },
  },
};
</script>

<style lang="scss">
.user-item {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  grid-template-rows: auto;
  align-items: center;
  column-gap: 0.5rem;
  &__name {
    font-size: 1.2rem;
    line-height: 143%;
  }
}
</style>
