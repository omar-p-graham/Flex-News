<template>
  <main class="about container">
    <div>
      <p>
        Flex News provides daily news articles at your finger tips on topics like Entertainment,
        Sports, Science, Technology, among others.
      </p>
      <p>
        This app fetches news articles via
        <a href="https://github.com/SauravKanchan/NewsAPI" target="_blank" rel="noopener noreferrer"
          >Saurav Kanchan - News API</a
        >.
      </p>
    </div>
  </main>
</template>

<style>
.about {
  min-height: 100vh;
  display: flex;
  align-items: start;
}

.about div {
  background: var(--card);
  width: 100%;
  padding: 4rem;
  border-radius: 0.375rem;
  margin-top: 6rem;
}

.about div p {
  font-size: large;
  margin-bottom: 1.2rem;
}

.about div p a {
  text-decoration: underline;
}
</style>
