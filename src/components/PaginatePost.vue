<script setup>
defineProps(["start", "end", "maxLength"]); //Propiedades.

const emit = defineEmits(["next", "previus"]); //Eventos a escuchar.
</script>
<template>
  <div class="btn-group" role="group" aria-label="Basic example">
    <button
      type="button"
      class="btn btn-primary"
      @click="emit('previus')"
      :disabled="start <= 0"
    >
      Previus {{ start }}
    </button>
    <button
      type="button"
      class="btn btn-primary"
      @click="emit('next')"
      :disabled="end >= 100"
    >
      Next {{ end }}
    </button>
  </div>
</template>
