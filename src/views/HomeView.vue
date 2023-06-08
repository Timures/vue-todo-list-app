<template>
  <main class="container users">

      <UsersList v-show="!showLoader" :users="users" />

      <LoaderSpinner v-show="showLoader" />
    
  </main>
</template>

<script>
import UsersList from '@/components/users/UsersList'
import LoaderSpinner from '@/components/common/LoaderSpinner'
export default {
  name: "HomeView",
  components: {
    UsersList,
    LoaderSpinner
  },
  data(){
    return {
      users: [],
      showLoader: false
    }
  },
  mounted() {
    this.fetchUsers();
  },
  methods: {
    fetchUsers() {
      this.showLoader = true
      fetch('https://jsonplaceholder.typicode.com/users?limit=10')
        .then(response => response.json())
        .then(data => {
          this.users = data; // Получаем только первые 10 пользователей
        })
        .catch(error => {
          console.error('Ошибка при получении пользователей:', error);
        });
        this.showLoader = false
    },
  },
};
</script>