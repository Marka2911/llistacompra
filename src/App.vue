<script setup>
import { ref } from 'vue';
import { computed } from 'vue';
import { onMounted } from 'vue';

const llista = ref(["patates", "pastanagues", "llimones", "pomes", "iogurts"]);
const nou = ref("");


const afegeixElement = () => {
  llista.value.push(nou.value)
  nou.value = ""

  localStorage["llistaCompra"] = JSON.stringify(llista.value);
}
const esborraElement = (index) => {
  llista.value.splice(index, 1)

  localStorage["llistaCompra"] = JSON.stringify(llista.value)
}

const elementValid = computed(() => {
  return nou.value.length > 0 && !llista.value.includes(nou.value)
})

onMounted( ()  => {
  if(localStorage["llistaCompra"]) {
    llista.value = JSON.parse(localStorage["llistaCompra"])
  }
})
</script>

<template>
  <h1>Llista de la compra</h1>
  <ul>
    <input type="text" placeholder="Que vols comprar" v-model="nou">
    <button @:click="afegeixElement" :disabled="nou.length == 0">Afegeix</button>
    <p v-if="llista.length > 0"> Hi ha {{ llista.length }} elements a la llista</p>
    <p v-else>La llista és buida</p>
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
