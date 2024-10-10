<script setup>
import { ref, computed } from "vue";

let contador = ref(0);
let favoritos = ref([]);

const incrementar = () => contador.value++;
const decrementar = () => contador.value--;
const reset = () => (contador.value = 0);
const añadir = () => favoritos.value.push(contador.value);

const claseContador = computed(() => {
  if (contador.value === 0) {
    return "cero";
  }
  if (contador.value > 0) {
    return "positivo";
  }
  if (contador.value < 0) {
    return "negativo";
  }
});

const bloquearBtnAñadir = computed(() => {
  const buscarNumero = favoritos.value.find((num) => num === contador.value);
  return buscarNumero || buscarNumero === 0;
});
</script>

<template>
  <body>
    <h1>Elige tus números favoritos</h1>
    <h3 :class="claseContador">{{ contador }}</h3>

    <button class="suma" @click="incrementar">Suma 1</button>
    <button class="resta" @click="decrementar">Resta 1</button>
    <button class="reset" @click="reset">Volver a 0</button>
    <button class="add" @click="añadir" :disabled="bloquearBtnAñadir">
      Añadir número
    </button>
    <br />
    <h4 v-for="num in favoritos">{{ num }}</h4>
  </body>
</template>

<style>
body {
  background-color: #ddd;
}

#app {
  text-align: center;
  margin-top: 50px;
}

h1 {
  font-weight: 600;
  font-size: 30px;
}
h3 {
  font-size: 40px;
  margin: 20px;
}
h4 {
  font-size: 34px;
  color: blue;
  margin-top: 8px;
}
.positivo {
  color: green;
}
.negativo {
  color: red;
}
.cero {
  color: black;
}
button {
  margin: 4px;

  height: 34px;
  border-radius: 10px;
  color: white;
  margin-bottom: 20px;
}
.suma {
  background-color: rgba(0, 128, 0, 0.428);
}
.resta {
  background-color: rgba(255, 0, 0, 0.466);
}
.reset {
  background-color: rgba(34, 125, 217, 0.671);
}
.add {
  color: black;
}
</style>
