<template>
  <v-card
    class="d-flex flex-column"
    elevation="5"
    width="344"
  >

    <div class="image-container">
      <v-img v-if="cat?.image?.url"
             height="100%"
             :src="cat?.image?.url"
             contain
      ></v-img>

      <v-card-title v-else class="d-flex align-center justify-center h-100">
        <v-icon size="100">mdi-cat</v-icon>
        Image not available
      </v-card-title>
    </div>

    <v-card-title>
      {{ cat.name }}
    </v-card-title>

    <v-card-subtitle>
      Origin: {{ cat.origin }}
    </v-card-subtitle>

    <v-card-text>
        They are known for been {{ cat.temperament }}
    </v-card-text>


    <v-card-actions class="mt-auto">
      <v-btn
        color="teal-accent-4"
        text="Read More"
        variant="text"
        @click="readMore = true"
      ></v-btn>
    </v-card-actions>

    <v-expand-transition>
      <v-card
        v-if="readMore"
        class="position-absolute w-100 d-flex flex-column justify-between"
        height="100%"
      >
        <v-card-text>
            {{ cat?.description }}
        </v-card-text>

        <v-card-actions class="pt-0">
          <v-btn
            color="teal-accent-4"
            text="Close"
            variant="text"
            @click="readMore = false"
          ></v-btn>
        </v-card-actions>
      </v-card>
    </v-expand-transition>
  </v-card>
</template>

<script>
import {toRaw} from "vue";

export default {
  props: {
    cat: {
      type: Object,
      required: true
    }
  },

  data: () => ({
    readMore: false,
  }),


  mounted() {
    toRaw(this.cat);
  }
};

</script>

<style scoped>
.image-container {
  height: 200px;
}
</style>




