<template>
    <div class="container">
      <div class="header-container">
        <h1>Search Wikipedia</h1>
      </div>

      <form @submit.prevent="submitSearch">
        <input
          v-model="search"
          type="text"
          id="search-input"
          placeholder="Enter search term"
        />
        <button type="submit">Search</button>
      </form>

      <div id="search-results">
        <div v-if="isLoading" class="spinner">Loading ...</div>
        <p v-if="error">{{ error }}</p>
        <div v-if="result.length">
          <div v-for="result in result" :key="result.pageid" class="result-item">
            <h3 class="result-title">
              <a
                :href="`https://en.wikipedia.org/?curid=${result.pageid}`"
                target="_blank"
                rel="noopener"
                >{{ result.title }}</a
              >
            </h3>
            <a
              :href="`https://en.wikipedia.org/?curid=${result.pageid}`"
              class="result-link"
              target="_blank"
              rel="noopener"
            >
              {{ `https://en.wikipedia.org/?curid=${result.pageid}` }}
            </a>
            <p class="result-snippet" v-html="result.snippet"></p>
          </div>
        </div>
      </div>
    </div>
</template>

<script setup>
import { ref } from "vue";

const search = ref('')
const result = ref([])
const isLoading = ref(false)
const error = ref('')

const searchWiki = async (query) => {
    const encodedQuery = encodeURIComponent(query)
    const endpoint = `https://en.wikipedia.org/w/api.php?action=query&list=search&prop=info&inprop=url&utf8=&format=json&origin=*&srlimit=10&srsearch=${encodedQuery}`

    try {
        isLoading.value = true;
        const response = await fetch(endpoint)
        const data = await response.json()

        if(data.query && data.query.search){
            result.value = data.query.search
            error.value = null
        } else {
            result.value = []
            error.value = 'No Result Found'
        }
    } catch (err) {
        console.log('Server Error ', err)
        result.value = []
        error.value = 'Error when fetching data'
    } finally {
        isLoading.value = false;
    }
}

const submitSearch = () => {
    if(search.value.trim() !== ''){
        searchWiki(search.value)
    } else {
        result.value = []
        error.value = 'Please enter valid search term'
    }
}

</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
}

h1 {
  font-size: 3rem;
  margin-bottom: 2rem;
}

#search-form {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 2rem;
}

#search-input {
  font-size: 1.2rem;
  padding: 0.5rem 1rem;
  margin-right: 1rem;
  border: 2px solid #ccc;
  border-radius: 0.25rem;
  flex-grow: 1;
}

#search-input:focus {
  outline: none;
  border-color: #0074d9;
}

button[type='submit'] {
  font-size: 1.2rem;
  padding: 0.5rem 1rem;
  background-color: #0074d9;
  color: #fff;
  border: none;
  border-radius: 0.25rem;
  cursor: pointer;
}

button[type='submit']:hover {
  background-color: #0063ad;
}

#search-results {
  margin-bottom: 2rem;
}

.result-item {
  margin-bottom: 1rem;
}

.result-title {
  font-size: 1.5rem;
  margin-top: 0;
}

.result-link {
  display: block;
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
  color: #0074d9;
}

.result-link:hover {
  text-decoration: underline;
}

.result-snippet {
  margin-top: 0;
}

.spinner {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2rem;
  height: 10rem;
}

</style>