<template>
  <my-navbar />
  <router-view />
</template>

<script>
import MyNavbar from '@/components/common/Navbar.vue'
export default {
  components: { MyNavbar }
}

</script>

<style>
@import url('@/assets/styles/global.scss');
</style>
