<script setup>
import { ref, onMounted } from "vue";
import { Dropzone } from "dropzone";

const dropRef = ref(null);

onMounted(() => {
  if (dropRef.value !== null) {
    new Dropzone(dropRef.value, {
      url: "http://localhost:5173/file",
      method: "POST",
    });
  }
});
</script>

<template>
  <div>
    <div ref="dropRef" class="dropzone"></div>
  </div>
</template>


<style lang="scss" scoped>
</style>