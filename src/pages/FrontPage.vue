<template>
  <div class="page-container h-100 d-flex flex-column">
    <ToolBar />
    <SearchBar :cats="cats" @search="filterCats" />

    <div v-if="error">
      <p>{{ error }}</p>
    </div>

    <div class="card-container" v-else>
      <CatCard class="ma-4" v-for="cat in filteredCats" :key="cat.id" :cat="cat" />
    </div>

  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from "@/components/SearchBar.vue";
import CatCard from "@/components/CatCard.vue";
import ToolBar from "@/components/ToolBar.vue";

export default {
  components: {ToolBar, CatCard, SearchBar},
  data() {
    return {
      cats: [],
      filteredCats: [],
      error: '',
    };
  },

  methods: {
    async fetchCatApi() {
      const url = 'https://api.thecatapi.com/v1/breeds?limit=100&page=0';
      const apiKey = 'live_HQ2p2jHlCzLlVWK1G8ZjfFbqZWzBHewj6VhHfrDpdx5DLCVO58PCKRFrq8kYJLdz';

      try {
        const response = await axios.get(url, {headers: {'x-api-key': apiKey}});

        if (response.status === 200) {
          this.cats = response.data;
          this.filteredCats = this.cats;
        } else {
          this.error = `Unexpected response status: ${response.status}, ${response.statusText}`;
        }
      } catch (error) {
        this.error = error;
      }
    },

    filterCats(search) {
      if (search) {
        this.filteredCats = this.cats.filter(cat => cat.name.includes(search));
      } else {
        this.filteredCats = this.cats;
      }
    }
  },

  created() {
    this.fetchCatApi();
  },
};
</script>

<style scoped>
.card-container {
  display: flex;
  justify-content: flex-start;
  flex-wrap: wrap;
}
</style>
