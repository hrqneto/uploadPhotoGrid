<!-- src/components/PhotoGrid.vue -->
<template>
  <div class="grid">
    <img
      v-for="(photo, index) in shuffledPhotos"
      :key="index"
      :src="photo.src"
      :alt="photo.name"
      class="grid-item"
    />
  </div>
</template>

<script setup>
import { ref, computed, watchEffect } from "vue";

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
}, 5000); // Ajuste esse valor para o intervalo de tempo desejado (em milissegundos)
</script>

<style>
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 1rem;
}

.grid-item {
  width: 100%;
  height: auto;
  object-fit: cover;
}
</style>
