<template>
  <div class="h-100 d-flex flex-column">
    <ToolBar/>
    <SearchBar class="pt-5 mx-15" :cats="cats" @search="filterCatName"/>

    <div v-if="error">
      <p>{{ error }}</p>
    </div>

    <div class="cats-container" v-else>
      <CatCard v-for="cat in filteredCats" :key="cat.id" :cat="cat"/>
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
      // Todo: API key should be stored in a .env file but for the sake of this exercise it's hardcoded.
      const apiKey = 'live_HQ2p2jHlCzLlVWK1G8ZjfFbqZWzBHewj6VhHfrDpdx5DLCVO58PCKRFrq8kYJLdz';

      try {
        const config = {
          headers: {
            'x-api-key': apiKey
          }
        };

        const response = await axios.get(url, config);

        if (response.status === 200) {
          this.cats = response.data;
          this.filteredCats = this.cats;
        } else {
          this.error = 'Something went wrong. Please try again later.';
        }
      } catch (error) {
        this.error = error;
      }
    },

    filterCatName(search) {
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
.cats-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
  gap: 20px;
  max-width: 100%;
  align-self: center;
  justify-items: center;
  padding-bottom: 20px;
}

.cats-container > *:only-child {
  grid-column: 1 / -1;
}
</style>
