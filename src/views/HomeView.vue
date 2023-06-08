<template>
  <main class="container users">
    <h1>Пользователи</h1>
    <div class="users-header">
      <h3>Имя</h3>
      <h3>Задачи</h3>
      <h3>Действие</h3>
    </div>
    <UsersList
      v-show="!showLoader"
      :users="users"
    />

    <LoaderSpinner v-show="showLoader" />
  </main>
</template>

<script>
import UsersList from "@/components/users/UsersList";
import LoaderSpinner from "@/components/common/LoaderSpinner";
export default {
  name: "HomeView",
  components: {
    UsersList,
    LoaderSpinner,
  },
  data() {
    return {
      users: [],
      showLoader: false,
    };
  },
  mounted() {
    this.fetchUsers();
  },
  methods: {
    fetchUsers() {
      this.showLoader = true;
      fetch("https://jsonplaceholder.typicode.com/users?limit=10")
        .then((response) => response.json())
        .then((data) => {
          this.users = data; // Получаем только первые 10 пользователей
        })
        .catch((error) => {
          console.error("Ошибка при получении пользователей:", error);
        });
      this.showLoader = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.users {
  max-width: 1024px;
  &-header {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr;
    grid-template-rows: auto;
    align-items: center;
    column-gap: 0.5rem;
    margin-bottom: 1rem;
    border-bottom: 1px solid #2c3e50;
    @media only screen and (max-width: 600px) {
      display: none;
    }
  }
}
</style>
