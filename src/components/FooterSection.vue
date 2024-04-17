<script setup>
const currentYear = new Date().getFullYear()
</script>

<template>
  <footer class="container">
    <p>&copy; Copyright {{ currentYear }} - Omar P. Graham</p>
  </footer>
</template>

<style scoped>
footer {
  border-top: 2px solid var(--border);
  width: 100%;
  /* position: absolute; */
  bottom: 0;
  font-size: 0.875rem;
  /* left: 50%;
  transform: translateX(-50%); */
  padding: 1.5rem 0;
  margin-top: 1.5rem;
}

footer p {
  text-align: center;
}
</style>
