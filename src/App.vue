<script setup>
import { onMounted, ref } from "vue";

import PaginatePost from "./components/PaginatePost.vue";
import BlogPost from "./components/BlogPost.vue";
import LoadingSpinner from "./components/LoadingSpinner.vue";

const posts = ref([]); //Guarda la data de la api.

const favorito = ref(""); //Guarda el titulo del post favorito.

//Funcion que cambia el titulo del post favorito.
const cambiarFavorito = (title) => {
  favorito.value = title;
};

const postXpage = 10; //Cantidad de posts que muestra por pantalla.
const start = ref(0); //Inicializa desde cero
const end = ref(postXpage); //Guarda la cantidad de posts actuales en pantalla.
const loading = ref(true); //Activa el spinner(loading) hasta que se carga la información.

//Method to go next from page.
const next = () => {
  start.value = start.value + postXpage;
  end.value = end.value + postXpage;
};

//Method to go back from page.
const previus = () => {
  start.value = start.value - postXpage;
  end.value = end.value - postXpage;
};

const fetchData = async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/posts");
    posts.value = await response.json();
  } catch (error) {
    console.log(error);
  } finally {
    loading.value = false;
  }
};

fetchData();
</script>

<template>
  <!--Muestro el loading hasta que la data este cargada. Una vez esta cargada el loading desaparece y muestra todos los posts.-->
  <LoadingSpinner v-if="loading" />
  <div class="container" v-else="loading">
    <h2 class="mt-5 mb-5 card text-bg-primary p-2">
      FAVORITE POST: {{ favorito }}
    </h2>

    <PaginatePost
      class="mb-2"
      :start="start"
      :end="end"
      @next="next"
      @previus="previus"
    />
    <!--Envio las props al componente correspondiente, en este caso (PaginatePost)-->

    <!--Obtengo los posts de cada objeto que se encuentra dentro del array y le asigno la clave y valor correspondiente.-->
    <!--Start contiene el valor incial del array de los posts y end contiene el valor final. Esto sirve para poder bloquear lost botones (next y previus)
    cuando (previus = 0) se bloquea el boton, y cuando (next = 100) tambien se bloquea.
    -->
    <BlogPost
      v-for="post in posts.slice(start, end)"
      :key="post.id"
      :id="post.id"
      :title="post.title"
      :body="post.body"
      @cambiarFavorito="cambiarFavorito"
      class="mb-2"
    ></BlogPost>
    <h3 class="mt-5 mb-5 card text-bg-primary p-2 d-flex col text-center">
      Web developer: Federico Maldonado
    </h3>
  </div>
</template>
