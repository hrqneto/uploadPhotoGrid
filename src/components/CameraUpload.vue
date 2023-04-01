<!-- src/components/CameraUpload.vue -->
<template>
  <div>
    <input
      ref="fileInput"
      type="file"
      accept="image/*"
      capture="environment"
      @change="handleFileChange"
      class="hidden"
    />
    <button @click="takePhoto" class="btn">Tirar foto ou fazer upload</button>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const fileInput = ref(null);
const emit = defineEmits(["photo-uploaded"]);

const takePhoto = () => {
  fileInput.value.click();
};

const handleFileChange = (event) => {
  const file = event.target.files[0];
  if (file) {
    emit("photo-uploaded", file);
  }
};
</script>

<style>
.btn {
  background-color: #1e90ff;
  color: white;
  padding: 8px 16px;
  border-radius: 4px;
}
</style>
