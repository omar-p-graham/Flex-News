<script setup>
import Filters from '../components/FilterSection.vue'
import { ref, onMounted } from 'vue'
import axios from 'axios'

const articles = ref(null)
const countryCode = ref('')
const theCategory = ref('')
const getNews = (country, category) => {
  countryCode.value = country
  theCategory.value = category
  let options = {
    method: 'GET',
    url: `https://saurav.tech/NewsAPI/top-headlines/category/${category}/${country}.json`
  }

  axios
    .request(options)
    .then(function (response) {
      articles.value = response.data
      console.log(response.data)
    })
    .catch(function (error) {
      console.error(error)
    })
}

const axis = (e) => {
  const x = e.pageX - e.target.offsetLeft
  const y = e.pageY - e.target.offsetTop

  e.target.style.setProperty('--xPos', x + 'px')
  e.target.style.setProperty('--yPos', y + 'px')
}

onMounted(() => {
  getNews('us', 'general')
})
</script>

<template>
  <div class="page-title container"><h1>FLEX NEWS</h1></div>
  <Filters @filter-search="getNews" />
  <main class="container">
    <div class="no-news" v-if="articles === null">
      <p>There are no news available at this time, please try again later.</p>
    </div>
    <div class="articles-container" v-else>
      <article class="news-card" v-for="(article, index) in articles.articles" :key="index">
        <div class="article-img">
          <img
            :src="article.urlToImage || './src/assets/newspaper.jpg'"
            :alt="`article-image-${index}`"
          />
        </div>
        <div class="article-details">
          <small>{{ article.publishedAt.substring(0, 10) }}</small>
          <h3>{{ article.title }}</h3>
          <p class="description">{{ article.description }}</p>
          <p>
            <span>Author(s): </span><br />
            {{ article.author }}
          </p>
          <p>
            <span>Source(s): </span><br />
            {{ article.source.name }}
          </p>
          <a :href="article.url" @mouseover="axis" target="_blank">
            <span>Read More</span>
          </a>
        </div>
      </article>
    </div>
  </main>
</template>

<style scoped>
.page-title {
  border-bottom: 2px solid var(--border);
  width: 100%;
}

.page-title h1 {
  text-align: center;
  font-size: 11.25rem;
  font-family: 'Playfair Display SC', serif;
}

main {
  margin-top: 2rem;
  margin-bottom: 2rem;
}

.no-news {
  display: grid;
  place-content: center;
  height: 40vh;
}

.no-news p {
  text-align: center;
  color: var(--primary);
  text-shadow: 0px 1px 2px var(--text);
  font-size: 1.5rem;
}

.articles-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 1fr;
  gap: 1.5rem;
  margin: 0;
  font-family: 'Ubuntu', sans-serif;
}

.news-card {
  background: var(--card);
  transition: all 0.5s ease-in-out;
  display: grid;
  grid-template-rows: 1fr 1.5fr;
  align-content: start;
  border-radius: 0.375rem;
}

.news-card:hover {
  box-shadow: 0px 15px 12px var(--shadow);
}

.news-card:hover .article-img img {
  transform: scale(1.1);
}

.news-card .article-img {
  overflow: hidden;
  border-radius: 0.375rem 0.375rem 0 0;
}

.news-card .article-img img {
  object-fit: cover;
  width: 100%;
  aspect-ratio: 16/9;
  transition: all 0.8s ease;
}

.news-card .article-details {
  padding: 0.5rem;
  display: grid;
  justify-content: center;
  align-content: space-between;
  gap: 0.8rem;
}

.news-card .article-details h3 {
  align-self: start;
}

.news-card .article-details span {
  font-weight: bold;
}

.news-card .article-details a {
  padding: 0.375rem 0.5rem;
  border: 1px solid var(--shadow);
  width: 100px;
  text-align: center;
  margin-bottom: 0.5rem;
  position: relative;
  overflow: hidden;
  align-self: end;
}

.news-card .article-details a:hover {
  border: 1px solid var(--text);
  box-shadow: 0px 15px 12px var(--shadow);
}

.news-card .article-details a::before {
  content: '';
  position: absolute;
  background-color: var(--primary);
  width: 0;
  height: 0;
  border-radius: 50%;
  left: var(--xPos);
  top: var(--yPos);
  transform: translate(-50%, -50%);
  transition:
    width 0.5s,
    height 0.5s;
}

.news-card .article-details a:hover::before {
  width: 300px;
  height: 300px;
}

.news-card .article-details a:hover span {
  font-weight: bold;
}

.news-card .article-details a span {
  position: relative;
  z-index: 1;
}

@media only screen and (max-width: 650px) {
  .page-title h1 {
    font-size: 7rem;
  }

  .articles-container {
    grid-template-columns: repeat(1, 1fr);
  }
}

@media only screen and (min-width: 651px) and (max-width: 768px) {
  .page-title h1 {
    font-size: 9rem;
  }

  .articles-container {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media only screen and (min-width: 768.01px) and (max-width: 991px) {
  .page-title h1 {
    font-size: 9.5rem;
  }

  .articles-container {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>
