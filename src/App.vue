<template>
  <div class="container text-center mt-3">
    <h1 :style="{ color: counterColor }">Hola {{ name.toUpperCase() }}</h1>
    <h2 :style="{ color: counterColor }">{{ counter }}</h2>
    <div class="btn group">
      <button @click="increment" class="btn btn-success">Incrementar</button>
      <button @click="decrement" class="btn btn-danger">Disminuir</button>
      <button @click="reset" class="btn btn-secondary">Resetear</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">
        Add
      </button>
    </div>
    <ul class="list-group mt-4">
      <li
        class="list-group-item"
        v-for="(num, index) in arrayFavoritos"
        :key="index"
      >
        {{ num }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const name = "Vue dinámico";

const counter = ref(0);
const arrayFavoritos = ref([]);

const increment = () => {
  counter.value++;
};

const decrement = () => {
  counter.value--;
};

const reset = () => {
  counter.value = 0;
};

const add = () => {
  arrayFavoritos.value.push(counter.value);
};

const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find((num) => num === counter.value);
  //if (numSearch === 0) return true;
  //return numSearch ? true : false;
  return numSearch || numSearch === 0;
});

/*const classCounter = computed(() => {
  if (counter.value === 0) {
    return "zero";
  }
  if (counter.vule > 0) {
    return "positive";
  }
  if (counter.value < 0) {
    return "negative";
  }
});*/

const counterColor = ref("black");

import { watch } from "vue";
watch(counter, (newValue) => {
  if (newValue < 0) {
    counterColor.value = "red";
  } else if (newValue > 0) {
    counterColor.value = "green";
  } else {
    counterColor.value = "black";
  }
});
</script>

<style>
/* Estilo para los botones, si es necesario */
button {
  margin: 5px;
}
</style>
