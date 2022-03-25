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

    <section class="container__btn">
      <button @mouseenter="retrait(10)">10€</button> &nbsp;
      <button @click="retrait(20)">20€</button> &nbsp;
      <button @click="retrait(40)">40€</button> &nbsp;
      <button @click="retrait(50)">50€</button> &nbsp;
      <button @click="retrait(60)">60€</button> &nbsp;
      <button @click="retrait(80)">80€</button> &nbsp;
      <button @click="retrait(100)">100€</button> &nbsp;
    </section>

    <p>{{ message }}</p>
  </fieldset>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

const TITLE = 'EXO 1';

// Configuration
const counter = ref(100);
const solde = ref(5000);
const operation = ref([]);

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

<style scoped lang="scss">
fieldset {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 20px;
  max-width: 450px;
  margin: 20px auto;

  legend {
    font-size: 1.5rem;
    font-weight: bold;
    padding: 0 10px;
  }
  section {
    &.container__btn {
      width: 100% -20px;
      border: 1px solid #ccc;
      border-radius: 5px;
      padding: 10px;
      display: flex;
      align-items: center;
      justify-content: space-evenly;
    }
  }
}

button {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 2.5px 10px;
  cursor: pointer;
}
</style>
