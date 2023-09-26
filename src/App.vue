<script setup>
import { ref, reactive, onMounted } from "vue";
import { db } from "./data/guitarras";
import GuitarraVue from "./components/Guitarra.vue";
import FooterVue from "./components/Footer.vue";
import HeaderVue from "./components/Header.vue";

const guitarras = ref([]);
const carrito = ref([]);

onMounted(() => {
  guitarras.value = db;
});

const agregarCarrito = (guitarra) => {
  const existeCarrito = carrito.value.findIndex((producto) => {
    producto.id === guitarra.id;
  });
  if (existeCarrito >= 0) {
    carrito.value[existeCarrito].cantidad++;
  } else {
    guitarra.cantidad = 1;
    carrito.value.push(guitarra);
  }
};

const decrementarCantidad = () => {};

const incrementarCantidad = () => {};
</script>

<template>
  <HeaderVue
    :carrito="carrito"
    @incrementar-cantidad="incrementarCantidad"
    @decrementar-cantidad="decrementarCantidad"
  />

  <main class="container-xl mt-5">
    <h2 class="text-center">Nuestra Colección</h2>

    <div class="row mt-5">
      <GuitarraVue
        v-for="guitarra in guitarras"
        :guitarra="guitarra"
        @agregar-carrito="agregarCarrito"
      />
    </div>
  </main>

  <FooterVue />
</template>
