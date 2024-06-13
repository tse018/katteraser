<template>
<div>
  <v-autocomplete
    :items="findCatName"
    class="mx-auto"
    menu-icon=""
    prepend-inner-icon="mdi-magnify"
    max-width="500"
    variant="solo"
    auto-select-first
    rounded
    label="Search for a cat breed"
    v-model="search"
    clearable
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
    },
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
