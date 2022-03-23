<script setup lang="ts">
import { ref, onMounted } from 'vue';

const TITLE = 'EXO 1';

// Configuration
const counter = ref(0);
const solde = ref(1500);

let message = ref('');

// Fonction pour retirer de l'argent.
function retrait(n: number) {
  if (solde.value > 0) {
    counter.value++;
    solde.value -= n;
    message.value = `Retrait de ${n} € effectué avec succès`;
    if (solde.value < 0) {
      solde.value = 0;
    }
  } else {
    message.value = 'Solde insuffisant';
  }
}

// Vérification au démarrage de la valeur du compteur.
onMounted(() => {
  console.log(
    `Le solde à l'initialisation de l'application est fixé à ${solde.value}`
  );
  console.log(
    `Le nombre d'opération à l'initialisation de l'application est fixé à ${counter.value}`
  );
});
</script>

<template>
  <fieldset>
    <legend>{{ TITLE }}</legend>

    <h2>Retrait dans une banque</h2>

    <ul>
      <li>Nombre d'opération effectué avant d'être à sec. {{ counter }}</li>
      <li>
        <b>Solde du compte courant : {{ solde }}</b>
      </li>
    </ul>

    <button @click="retrait(10)">10€</button> &nbsp;
    <button @click="retrait(20)">20€</button> &nbsp;
    <button @click="retrait(40)">40€</button> &nbsp;
    <button @click="retrait(50)">50€</button> &nbsp;
    <button @click="retrait(60)">60€</button> &nbsp;
    <button @click="retrait(80)">80€</button> &nbsp;
    <button @click="retrait(100)">100€</button> &nbsp;

    <p>{{ message }}</p>
  </fieldset>
</template>

<style>
fieldset {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  max-width: calc(max-content + 20px);
  margin: 20px auto;
}
legend {
  font-size: calc(1em + 1vw);
  font-weight: bold;
  padding: 0 10px;
}
</style>
