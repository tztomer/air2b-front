<template>
  <span class="shadow-left"></span>
  <carousel :transition="330" :items-to-show="20" snapAlign="start">
    <slide v-for="(label, idx) in labelsList" ref="labels" :key="label" @click="filter(label.propertyType)">
      <div class="labels">
        <img class="property-type-img" :src="utilService.getImgUrlFilter(label.src)" />
        <span>{{ label.propertyType }}</span>
      </div>
    </slide>

    <template #addons>
      <span class="shadow-right"></span>
      <navigation ref="el" />
    </template>
  </carousel>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const el = ref();

onMounted(() => {
  const prev = document.querySelector('.carousel__prev');
  prev.style.visibility = 'hidden';
  const next = document.querySelector('.carousel__next');
  next.addEventListener('click', e => {
    prev.style.visibility = 'visible';
  });
});
</script>

<script>
import 'vue3-carousel/dist/carousel.css';
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel';
import { utilService } from '../services/util.service.js';

export default {
  name: 'explore-labels',
  data() {
    return {
      labelsList: null,
      filterBy: {
        propertyType: [],
      },
      index: null,
    };
  },
  methods: {
    filter(value) {

      this.filterBy.propertyType = []
      this.filterBy.propertyType.push(value)
      this.$store.dispatch({ type: 'setFilterBy', filterBy: this.filterBy });
    },
  },

  created() {
    this.labelsList = this.$store.getters.getLabels;
  },
  computed: {

  },
  components: {
    Carousel,
    Slide,
    Pagination,
    Navigation,
  },
};
</script>
