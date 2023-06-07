<template>
  <main class="container users">
    <h1>Пользователи</h1>
    <UsersList :users="users" />
  </main>
</template>

<script>
import UsersList from '@/components/users/UsersList'
export default {
  name: "HomeView",
  components: {
    UsersList
  },
  data(){
    return {
      users: []
    }
  },
  mounted() {
    this.fetchUsers();
  },
  methods: {
    fetchUsers() {
      fetch('https://jsonplaceholder.typicode.com/users?limit=10')
        .then(response => response.json())
        .then(data => {
          this.users = data; // Получаем только первые 10 пользователей
        })
        .catch(error => {
          console.error('Ошибка при получении пользователей:', error);
        });
    },
  },
};
</script>