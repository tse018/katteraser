<template>
  <v-pagination class="pagination" :length="length"></v-pagination>
</template>

<script>
export default {
  props: {
    currentPage: {
      type: Number,
      required: true
    },
    length: {
      type: Number,
      required: true
    }
  }
};
</script>

<style scoped>

</style>

