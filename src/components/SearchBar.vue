<template>
<div>
  <v-autocomplete
    :items="findCatName"
    class="mx-auto"
    density="comfortable"
    menu-icon=""
    prepend-inner-icon="mdi-magnify"
    style="max-width: 350px;"
    theme="light"
    variant="solo"
    auto-select-first
    item-props
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
