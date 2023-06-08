<template>
  <div class="loader-spinner">
    Загрузка...
    <div class="spinner"></div>
  </div>
</template>

<script>
export default {
    name: "loader-spinner"
}
</script>

<style scoped>
.loader-spinner {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  flex-direction: column;
  row-gap: 1rem;
}

.spinner {
  width: 50px;
  height: 50px;
  border: 5px solid #ccc;
  border-top-color: #666;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>