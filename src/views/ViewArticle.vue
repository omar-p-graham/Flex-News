<script setup>
import { useRoute, useRouter } from 'vue-router'
import { ref } from 'vue'
const route = useRoute()
const router = useRouter()
const article = ref(null)
import axios from 'axios'

const getNews = (country, category, index) => {
  let options = {
    method: 'GET',
    url: `https://saurav.tech/NewsAPI/top-headlines/category/${category}/${country}.json`
  }

  axios
    .request(options)
    .then(function (response) {
      article.value = response.data.articles[index]
    })
    .catch(function (error) {
      console.error(error)
    })
}

getNews(route.params.country, route.params.category, route.params.id)
</script>

<template>
  <main class="container">
    <section>
      <div class="article-img">
        <img
          :src="article.urlToImage || './src/assets/newspaper.jpg'"
          :alt="`article-image-${route.params.id}`"
        />
      </div>
      <div class="article-details">
        <h2>{{ article.title }}</h2>
        <p>{{ article.content }}</p>
      </div>
    </section>
    <aside>
      <div class="metadata">
        <h6>Publisshed</h6>
        <p>{{ article.publishedAt.substring(0, 10) }}</p>
      </div>
      <div class="metadata">
        <h4>Author(s)</h4>
        <p>{{ article.author }}</p>
      </div>
      <div class="metadata">
        <h6>Source(s)</h6>
        <p v-for="source in article.source" :key="source.id">{{ source.name }}</p>
      </div>
    </aside>
  </main>
</template>

<style scoped>
main {
  display: flex;
  gap: 1.875rem;
  height: 100vh;
}
</style>
