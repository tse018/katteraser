<template>
  <v-card
    class="d-flex flex-column"
    elevation="5"
    width="344"
    height="450"
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
      They are known for been {{ cat.temperament }}.
      This cat has social needs rated at {{ cat.social_needs }}.
      It is {{ cat.stranger_friendly }} in terms of friendliness towards strangers.
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
        <v-card-text class="image-container">
          {{ cat?.description }}
          <br>
          <br>
          The cat weighs {{ cat.weight.metric }} kilograms in the metric system and {{ cat.weight.imperial }} pounds in
          the imperial system. This cat requires a {{ cat.grooming }} level of grooming. It has an affection level of
          {{ cat.affection_level }} and an energy level of {{ cat.energy_level }}. The cat is quite intelligent with an
          intelligence level of {{ cat.intelligence }}, and it has an adaptability level of {{ cat.adaptability }}.
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




