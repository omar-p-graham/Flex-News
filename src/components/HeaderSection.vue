<script setup>
import { RouterLink } from 'vue-router'
</script>

<template>
  <header class="container">
    <div class="menu-bar">
      <div class="logo-container">
        <img alt="Vue logo" class="logo" src="@/assets/news-logo.svg" width="30" height="30" />
      </div>
      <nav>
        <RouterLink activeClass="active" to="/">Home</RouterLink>
        <RouterLink activeClass="active" to="/about">About</RouterLink>
      </nav>
    </div>
  </header>
</template>

<style scoped>
header {
  margin-top: 2rem;
  width: 100%;
}

header.container .menu-bar {
  display: flex;
  justify-content: space-between;
  align-content: center;
  font-size: 1.625rem;
  border-top: 2px solid var(--border);
  border-bottom: 2px solid var(--border);
  padding-top: 5px;
  padding-bottom: 5px;
}

header.container nav {
  display: flex;
  gap: 1rem;
}

header.container nav a {
  font-family: 'Playfair Display SC', serif;
}

header.container nav a.active,
header.container nav a:hover {
  color: var(--primary);
  font-weight: 700;
}
</style>
