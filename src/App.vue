<template>
  <section class="container">
    <Navbar />
    <section class="selected">
      <fieldset>
        <legend>Sélectionnez un choix</legend>
        <p>
          Apprentissage des notions de vue via différents composants qui peuvent
          être sélectionné ci-dessous
        </p>
        <select name="exo" id="exo" v-model="choix">
          <optgroup label="Bascule sur un quelconque exercice">
            <option selected value="null">voir la liste</option>
            <option value="exo1">Exercice 1 : ref + onMounted</option>
            <option value="exo2">Exercice 2 : ref + reactive + computed</option>
          </optgroup>
        </select>
      </fieldset>
    </section>

    <section class="exos">
      <template v-if="choix === 'null'">
        <fieldset>
          <p>Aucun exercice sélectionné</p>
        </fieldset> 
      </template>
      <template v-else-if="choix === 'exo1'">
        <Exo1 />
      </template>
      <template v-else-if="choix == 'exo2'">
        <Reactive />
      </template>
    </section>
  </section>
</template>

<script setup lang="ts">
// Dépendances
import { ref } from 'vue';

// Component Navbar
import Navbar from './components/Navbar/Navbar.vue';

// Components Exercices
import Exo1 from './components/Exercices/Exo1/Exo1.vue';
import Reactive from './components/Exercices/Exo2/Reactive.vue';

// Logique
const choix = ref('null');
</script>

<style lang="scss">
body {
  margin: 0;
  background-color: #444;
  color: #fff;
  min-height: 100vh;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: auto 1fr;
  grid-template-areas:
    'navbar'
    'container';

  section {
    &.container {
      grid-area: container;
      display: grid;
      grid-template-columns: 1fr;
      grid-template-rows: 1fr auto;
      grid-template-areas:
        'selected'
        'exos';

      section {
        &.selected {
          fieldset {
            grid-area: selected;
            max-width: 65%;
            margin: 50px auto;
            padding: 0 25px 25px;
            border: 1px solid #ccc;
            border-radius: 5px;

            legend {
              font-size: 1.5rem;
              font-weight: bold;
              padding: 0 10px;
            }
            p {
              font-size: 1rem;
              font-style: italic;
              color: lightcyan;
              line-height: 1.5;
            }

            select {
              grid-area: select;
              width: 100%;
              border: 1px solid #ccc;
              border-radius: 3px;
              padding: 10px;
              font-size: 1.2rem;
              font-weight: bold;
              color: #444;
              background-color: #fff;
              cursor: pointer;

              optgroup {
                font-size: 1.2rem;
                font-weight: bold;
                padding: 0 10px;
                color: #444;
              }
            }
          }
        }
      }
      &.exos {
        grid-area: exos;
      }
    }
  }
}

fieldset {
  max-width: 80%;
  margin: 20px auto;
  text-align: center;
}
</style>
