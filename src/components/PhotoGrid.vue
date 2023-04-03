<!-- src/components/PhotoGrid.vue -->
<template>
  <div class="container">
    <div class="grid">
      <template v-for="(photo, index) in shuffledPhotos" :key="index">
        <div class="grid-item-wrapper">
          <img :src="photo.src" :alt="photo.name" class="grid-item" />
        </div>
        <div class="grid-item-wrapper">
          <img
            :src="index % 2 === 0 ? bloco1 : bloco2"
            alt="Block"
            class="grid-item"
          />
        </div>
      </template>
    </div>
  </div>
</template>

<script setup>
import { ref, watchEffect } from "vue";
import bloco1 from "../assets/bloco1.png";
import bloco2 from "../assets/bloco2.png";

const props = defineProps({
  photos: {
    type: Array,
    required: true,
  },
});

const shuffledPhotos = ref([]);

const shuffleArray = (array) => {
  return array.slice().sort(() => Math.random() - 0.5);
};

watchEffect(() => {
  shuffledPhotos.value = shuffleArray(props.photos);
});

setInterval(() => {
  shuffledPhotos.value = shuffleArray(props.photos);
}, 5000);
</script>

<style>
.container {
  width: 980px;
  height: 700px;
  background-color: transparent;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 1rem;
}

.grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 0.3rem;
}

.grid-item-wrapper {
  width: 200px;
  height: 200px;
}

.grid-item {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>
