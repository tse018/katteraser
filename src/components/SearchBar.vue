<template>
  <div>
    <v-autocomplete
      clearable
      label="Search"
      :items="findCatName"
      v-model="search"
    ></v-autocomplete>
  </div>
</template>

<script>
export default {
  props: {
    cats: {
      type: Array,
      required: true
    }
  },

  data() {
    return {
      search: null,
    };
  },

  computed: {
    findCatName() {
      return this.cats.map(cat => cat.name);
    }
  },

  watch: {
    search() {
      this.$emit('search', this.search);
    }
  }
};
</script>


<style scoped>
</style>
