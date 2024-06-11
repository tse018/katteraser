<template>
  <v-pagination :length="length"></v-pagination>
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
