<script setup>
import { ref, defineEmits } from 'vue'

const emit = defineEmits(['filterSearch'])
const country = ref('us')
const category = ref('general')
const categories = [
  'general',
  'business',
  'entertainment',
  'health',
  'science',
  'sports',
  'technology'
]
const countries = [
  { name: 'USA', code: 'us' },
  { name: 'Russia', code: 'ru' },
  { name: 'United Kingdom', code: 'gb' },
  { name: 'India', code: 'in' },
  { name: 'France', code: 'fr' },
  { name: 'Australia', code: 'au' }
]

const getParams = (country, category) => {
  emit('filterSearch', country, category)
}
</script>

<template>
  <div class="container">
    <div class="filters">
      <div class="filter">
        <label for="countries">Country</label>
        <select name="countries" id="countries" v-model="country">
          <option v-for="country in countries" :key="country.code" :value="country.code">
            {{ country.name }}
          </option>
        </select>
      </div>
      <div class="filter">
        <label for="categories">Category</label>
        <select name="categories" id="categories" v-model="category">
          <option v-for="category in categories" :key="category" :value="category">
            {{ category }}
          </option>
        </select>
      </div>
      <div class="filter">
        <label for="getNewsBtn"></label>
        <button type="button" id="getNewsBtn" @click="getParams(country, category)">
          Get News
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.filters {
  margin-top: 1rem;
  padding: 1rem 0;
  border-radius: 0.375rem;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-content: center;
  gap: 0.8rem;
  background-color: var(--card);
  width: 100%;
  box-shadow: 0px 7px 28px var(--shadow);
}

.filters button {
  padding: 0.2rem 1rem;
  text-transform: capitalize;
  border-radius: 0.5rem;
  border: 1px solid var(--gray-lighter);
  outline: none;
  background: var(--white);
}

.filter button:hover {
  background: var(--primary);
  border: 1px solid var(--gray-darker);
  box-shadow: 0px 7px 28px var(--shadow);
  font-weight: 900;
  cursor: pointer;
}

.filter {
  display: grid;
  width: 15.625rem;
  padding: 3px 8px;
}

.filter :is(label, select, button) {
  font-family: 'Ubuntu', sans-serif;
  font-size: 0.875rem;
}
.filter select {
  padding: 0.5rem 1rem;
  text-transform: capitalize;
  width: 100%;
}

@media only screen and (max-width: 650px) {
  .filter {
    width: 100%;
  }
}
</style>
