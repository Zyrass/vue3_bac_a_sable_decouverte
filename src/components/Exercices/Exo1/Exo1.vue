<template>
  <section class="child">
    <h1>{{ state.title }}</h1>
    <p>{{ state.description }}</p>

    <fieldset>
      <legend>SOLDE : {{ solde }} €</legend>

      <h2>Choisissez le montant désiré</h2>

      <span>
        Nombre d'opération effectué avant d'être à sec. {{ counterInit }}
      </span>

      <section class="container__btn">
        <button @click="retrait(10)">10€</button>
        <button @click="retrait(60)">60€</button>
        <button @click="retrait(20)">20€</button>
        <button @click="retrait(80)">80€</button>
        <button @click="retrait(40)">40€</button>
        <button @click="retrait(100)">100€</button>
        <button @click="retrait(50)">50€</button>
        <button disabled>autre</button>
      </section>

      <p class="alert alert-success" v-if="retraitPossible">
        {{ solde == 1000 ? '' : messageSuccess }}
      </p>
      <p class="alert alert-danger" v-else>{{ messageError }}</p>
    </fieldset>
  </section>
</template>

<script setup lang="ts">
import { reactive, ref, onMounted } from 'vue';

// Configuration des informations relatives à l'exercice souhaité
const state = reactive({
  title: 'Exercice n°1',
  description:
    'Découverte de ref, onMounted via un exercice de simulation de distributeur de billet de banque.',
});

// Configuration des références
const counterInit = ref(0);
const solde = ref(1000);
const messageSuccess = `Le retrait de à été réalisé avec succès.`;
const messageError = `Le retrait n'a pas été réalisé, solde insuffisant.`;
const retraitPossible = ref(true);

/**
 * Cette fonction permet de retirer de l'argent du compte courant.
 * @param n [number] : montant à retirer
 */
function retrait(n: number) {
  if (solde.value > 0) {
    counterInit.value++;
    solde.value -= n;

    if (solde.value < 0) {
      retraitPossible.value = false;
      solde.value = 0;
    }
  } else {
    retraitPossible.value = false;
  }
}

// Vérification au démarrage de la valeur du compteur.
onMounted(() => {
  console.log(
    `Le solde à l'initialisation de l'application est fixé à ${solde.value}`
  );
  console.log(
    `Le nombre d'opération à l'initialisation de l'application est fixé à ${counterInit.value}`
  );
});
</script>

<style scoped lang="scss">
section {
  &.child {
    padding: 20px 40px;
    background-color: mediumseagreen;
    height: 100%;

    fieldset {
      position: relative;
      border: 1px solid #ccc;
      border-radius: 5px;
      padding: 20px;
      min-width: 90%;
      margin: 20px;

      legend {
        font-size: 1.5rem;
        font-weight: bold;
        padding: 0 10px;
      }

      span {
        position: absolute;
        top: 0px;
        right: 20px;
        font-size: 0.8rem;
        font-style: italic;
        color: lightcyan;
      }

      section {
        &.container__btn {
          width: 100% -20px;
          border: 1px solid #ccc;
          border-radius: 5px;
          padding: 10px;
          display: grid;
          grid-template-columns: repeat(2, 1fr);
          grid-gap: 10px;
        }
      }
    }

    .alert {
      padding: 10px 20px;
      font-size: 1.2rem;
      font-weight: bold;

      &-success {
        color: rgb(242, 255, 0);
      }
      &-danger {
        color: rgb(109, 16, 16);
      }
    }

    button {
      border: 1px solid #ccc;
      border-radius: 5px;
      padding: 2.5px 10px;
      cursor: pointer;
    }
  }
}
</style>
