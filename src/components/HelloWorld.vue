<script setup lang="ts">
defineProps<{
  msg: string
}>()
</script>

<template>
  <div class="container mt-5">
    <!-- About Me Section -->
    <div class="card shadow-lg">
      <div class="card-header bg-primary text-white">
        <h1 class="mb-0">Contact Book</h1>
      </div>
      <div class="card-body">
        <p class="card-text lead">
          <h2>Hello! My name is <strong>Inderjot Kaur</strong>. I am a passionate web developer learning new technologies
          like Vue.js and Vite. I enjoy creating dynamic and user-friendly web applications.</h2>
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 700;
  font-size: 3rem;
}

h3 {
  font-size: 1.3rem;
  margin-top: 10px;
}

.card {
  border-radius: 15px;
}

.card-header {
  border-top-left-radius: 15px;
  border-top-right-radius: 15px;
}

.list-group-item {
  font-size: 1.1rem;
}

@media (min-width: 768px) {
  h1 {
    font-size: 3.5rem;
  }

  h3 {
    font-size: 1.5rem;
  }
}
</style>
