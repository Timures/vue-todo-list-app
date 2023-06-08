<template>
  <nav class="main-nav">
    <h1>Timures</h1>
    <ul>
      <li>
        <router-link to="/">Пользователи</router-link>
      </li>
      <li>
        <router-link to="/payments">Платежи</router-link>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "my-navbar",
};
</script>

<style lang="scss">
@import "@/assets/styles/_variables.scss";

.main-nav {
  border-bottom: 1px solid #2c3e50;;
  padding: 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;

  h1 {
    color: $main;
    font-size: 1.3rem;
    line-height: 123%;
  }

  ul {
    display: flex;
    column-gap: 1rem;
    list-style-type: none;
  }
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  text-decoration: none;
  &:hover {
    color: $link_hover;
  }
  &:visited {
    color: $link_visited;
  }
}

nav a.router-link-exact-active {
  color: $link_active;
}
</style>
