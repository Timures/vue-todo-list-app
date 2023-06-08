<template>
  <div class="user-item">
    <div class="user-item__name">
      <span>Имя: </span>{{ user.name }}
    </div> 
    <MyButton
      :disabled="false"
      @click="showModalUserTodos(user.id)"
    >
      Задачи
    </MyButton>
    <MyButton
      :disabled="false"
      @click="showModalUserEdit(user.id)"
    >
      Редактировать
    </MyButton>
  </div>

  <Modal
    :visible="isModalTodosVisible"
    @close="closeModal"
  >
    <template #header>
      <h3>Задачи пользователя: {{ user.name }}</h3>
    </template>
    <template #body>
      <TodosList :todos="userTodos" />
    </template>
    <template #footer>
      <MyButton
        :disabled="false"
        :size="'small'"
        @click="closeModal"
      >
        Закрыть
      </MyButton>
    </template>
  </Modal>

  <Modal
    :visible="isModalVisible"
    @close="closeModal"
  >
    <template #header>
      <h3>Редактировать пользователя</h3>
    </template>
    <template #body>
      <form
        class="user-form"
        @submit.prevent="updateUser(user.id)"
      >
        <div class="form-group">
          <label for="name">Имя</label>
          <input
            id="name"
            v-model="userData.name"
            type="text"
            required
          >
        </div>
        <div class="form-group">
          <label for="phone">Номер телефона</label>
          <input
            id="phone"
            v-model="userData.phone"
            type="tel"
            required
          >
        </div>
        <div class="form-group">
          <label for="email">Email</label>
          <input
            id="email"
            v-model="userData.email"
            type="email"
            required
          >
        </div>
        <div class="form-actions">
          <MyButton
            :disabled="false"
            type="submit"
          >
            Сохранить
          </MyButton>
        </div>
      </form>
    </template>
    <template #footer>
      <MyButton
        :disabled="false"
        :size="'small'"
        @click="closeModal"
      >
        Закрыть
      </MyButton>
    </template>
  </Modal>
</template>

<script>
import Modal from "@/components/common/MyModal";
import TodosList from "@/components/todos/TodosList.vue";
import MyButton from "@/components/common/UI/MyButton";
export default {
  name: "UserItem",
  components: {
    Modal,
    TodosList,
    MyButton
  },
  props: {
    user: {
      type: Object,
      default: () => {},
    },
  },
  emits:['update'],
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
  methods: {
    updateUser(user_id){
      this.$emit('update', user_id, this.userData)
      // console.log('user update ', user_id);
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
      // console.log('user name ', user_id);
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

  @media only screen and (max-width: 600px) {
    grid-template-columns: auto;
    grid-template-rows: auto auto;
    row-gap: 0.5rem;
  }
  &__name {
    font-size: 1.2rem;
    line-height: 143%;
    span {
      display: none;
    }
    @media only screen and (max-width: 600px) {
      span {
        display: inline-block;
        font-size: 1rem;
        font-weight: normal;
      }
      font-weight: bold;
    }
  }
}

.user-form {
  max-width: 500px;
  margin: 0 auto;
}

.form-group {
  margin-bottom: 20px;
  display: grid;
  align-items: center;
  grid-template-columns: 1fr 2fr;
  column-gap: 00.5rem;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
  text-align: right;
}

input[type="text"],
input[type="tel"],
input[type="email"] {
  // width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.form-actions {
  display: flex;
  justify-content: flex-end;
}
</style>
