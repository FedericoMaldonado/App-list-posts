<script setup>
defineProps(["loading"]);
</script>

<template>
  <div
    class="d-flex flex-column align-items-center justify-content-center mt-5 text-primary"
  >
    <div class="spinner-border" role="status">
      <span class="visually-hidden">Loading...</span>
    </div>
    <p class="text-center mt-2">Loading...</p>
  </div>
</template>
