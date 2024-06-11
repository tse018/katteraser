<template>

  <ToolBar />

  <SearchBar :cats="cats" @search="filterCats" />

  <div v-if="error">
    <p>{{ error }}</p>
  </div>

  <div class="card-container" v-else>
    <CatCard v-for="cat in filteredCats" :key="cat.id" :cat="cat" />
  </div>

  <Pagination v-model="currentPage" :length="cats.length"  current-page="0"/>


  <Footer />
</template>

<script>
import axios from 'axios';
import SearchBar from "@/components/SearchBar.vue";
import CatCard from "@/components/CatCard.vue";
import ToolBar from "@/components/ToolBar.vue";
import Footer from "@/components/Footer.vue";
import Pagination from "@/components/Pagination.vue";
import { chunk } from "lodash";

export default {
  components: {Pagination, Footer, ToolBar, CatCard, SearchBar},
  data() {
    return {
      cats: [],
      filteredCats: [],
      error: '',
      currentPage: 1,
    };
  },

  methods: {
    async fetchCatApi() {
      const url = 'https://api.thecatapi.com/v1/breeds?limit=100&page=0';
      const apiKey = 'live_HQ2p2jHlCzLlVWK1G8ZjfFbqZWzBHewj6VhHfrDpdx5DLCVO58PCKRFrq8kYJLdz';

      try {
        const response = await axios.get(url, {headers: {'x-api-key': apiKey}});

        if (response.status === 200) {
          this.cats = chunk(response.data, 8);
          this.filteredCats = this.cats[this.currentPage - 1];
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
        this.filteredCats = this.cats[this.currentPage - 1].filter(cat => (cat.name, search));
      } else {
        this.filteredCats = this.cats[this.currentPage - 1];
      }
    },
  },

  watch: {
    currentPage() {
      this.filterCats(this.search);
    }
  },

  created() {
    this.fetchCatApi();
  },

  mounted() {
    this.filteredCats = this.cats;
  },
};
</script>


<style scoped>
  .card-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
</style>
