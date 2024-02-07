<script setup>
//Defino el tipo de dato para cada una de las props.
defineProps({
  id: Number,
  title: String,
  body: String,
});

const emit = defineEmits(["cambiarFavorito"]);
</script>

<template>
  <div class="card bg-light bg-gradient">
    <div class="card-body">
      <!--Muestro el id y titulo de cada uno de los posts-->
      <h2 class="card-title">{{ id }} - {{ title }}</h2>
      <h5>
        {{ body }}
      </h5>

      <!--Cuando presione el boton el emit escucha el evento del metodo (cambiarFavorito) y muestra el titulo-->
      <button
        @click="emit('cambiarFavorito', title)"
        class="btn btn-outline-primary"
      >
        Favorite
      </button>
    </div>
  </div>
</template>
