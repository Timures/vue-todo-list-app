<template>
  <ul class="users-list">
    <li v-for="user in users"
      :key="user.id">
      <UserItem :user="user" />
      <hr />
    </li>
  </ul>
</template>

<script>
import UserItem from "@/components/users/UserItem";
export default {
  name: "UsersList",
  props: {
    users: {
      type: Object,
      default: ()=>{}
    }
  },
  components: { UserItem },
};
</script>

<style lang="scss">
.users-list {
  list-style-type: none;
  margin: 0;
  padding: 0;
  li {
    &:not(:last-child){
      margin-bottom: 0.5rem;
    }
  }
}
</style>
