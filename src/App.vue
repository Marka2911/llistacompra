<script setup>
import { ref } from 'vue';
import { computed } from 'vue';
const llista = ref(["patates", "pastanagues", "llimones", "pomes", "iogurts"]);
const nou = ref("");


const afegeixElement = () => {
  llista.value.push(nou.value)
  nou.value = ""
}
const esborraElement = (index) => {
  llista.value.splice(index, 1)
}

const elementValid = computed(() => {
  return nou.value.length > 0 && !llista.value.includes(nou.value)
})
</script>

<template>
  <h1>Llista de la compra</h1>
  <ul>
    <input type="text" placeholder="Que vols comprar" v-model="nou">
    <button @:click="afegeixElement" :disabled="!elementValid">Afegeix</button>
    <li v-for="(producte, index) in llista">
      <button @:click="esborraElement(index)">🗑️</button>
      {{ producte }}
    </li>
  </ul>
</template>

<style scoped>
* {
  font-family: Arial, Helvetica, sans-serif;
}

li {
  font-size: 1.5em;
}

input,
button {
  font-size: 2em;
  padding: 0.25em 0.5em;
}
</style>
