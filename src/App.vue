<template>
  <div class="container">
    <div v-if="photos.length" class="mt-8">
      <PhotoGrid :photos="photos" />
    </div>
    <CameraUpload @photo-uploaded="addPhoto" />
  </div>
</template>

<script setup>
import { ref } from "vue";
import CameraUpload from "./components/CameraUpload.vue";
import PhotoGrid from "./components/PhotoGrid.vue";

const photos = ref([]);

const addPhoto = async (file) => {
  const reader = new FileReader();
  reader.onload = (event) => {
    photos.value.push({ src: event.target.result, name: file.name });
  };
  reader.readAsDataURL(file);
};
</script>

<style>
.mt-8 {
  margin-top: 2rem;
}
</style>
