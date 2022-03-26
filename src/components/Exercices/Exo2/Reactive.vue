<template>
  <section class="exo2">
    <h1>Bonjour {{ state.prenom }}</h1>

    <fieldset>
      <legend>{{ state.product.ref }}</legend>
      <h2>{{ state.product.name }}</h2>
      <hr />
      <blockquote>{{ state.product.description }}</blockquote>
      <hr />
      <section class="price">
        <span>
          <strong>Prix TTC: </strong>{{ prixProductTTC.toFixed(2) }} €</span
        >
        <span>
          <strong>Prix HT : </strong>{{ prixProductHT.toFixed(2) }} €</span
        >
      </section>

      <br />

      <small>
        Quantitée disponible :
        {{
          state.product.quantity > 0
            ? state.product.check_quantity - state.product.quantity
            : state.product.check_quantity
        }}
      </small>

      <section class="quantity">
        <label for="add_product">Combien de formation souhaitez-vous ? </label>
        <input
          type="number"
          min="0"
          :max="state.product.check_quantity"
          v-model="state.product.quantity"
        />
      </section>
    </fieldset>
  </section>
</template>

<script setup lang="ts">
import { reactive, computed } from 'vue';

let state = reactive({
  prenom: 'Alain',
  product: {
    ref: 'formation-vue-js',
    description:
      'Vous y apprendrez à utiliser le framework Vue dans sa toute dernière version',
    name: 'Formation Vue.js',
    price: 19.99,
    quantity: 0,
    check_quantity: 12,
  },
});

const prixProductHT = computed(
  () => state.product.price * state.product.quantity
);
const prixProductTTC = computed(() => prixProductHT.value * 1.2);

setTimeout(() => {
  state.prenom = 'I-Love-Vue';
  console.log('prenom', state.prenom);
}, 2000);
</script>

<style scoped lang="scss">
section {
  &.exo2 {
    background-color: mediumseagreen;
    padding: 20px 30px;
    height: 100%;
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: auto 1fr;

    h1 {
      color: #fff;
      font-size: 2rem;
      font-weight: bold;
      text-align: center;
      text-shadow: 1px 1px #444;
      border-bottom: 16px solid #444;
      box-shadow: 0 0 5px #444;
      width: 50%;
      padding: 10px 0;
      margin: 20px auto;
    }

    fieldset {
      border: 1px solid #444;
      padding: 0 20px 20px;
      margin: 0px auto 30px;      
      border-radius: 5px;
      box-shadow: 3px 3px 6px #444;
      position: relative;

      blockquote {
        border-left: 5px solid #444;
        padding: 10px 20px;
        margin: 10px;
        color: #fff;
        text-shadow: 1px 1px #444;
        text-align: left;
        font-style: italic;
        letter-spacing: 1.8px;
      }

      legend {
        font-size: 1.2rem;
        font-weight: bold;
        padding: 20px;
        text-transform: uppercase;
        color: #444;
        text-align: left;
      }
      section.price {
        display: flex;
        justify-content: space-between;
        background: #444;
        border-radius: 3px;
        padding: 10px;
      }
      section.price span {
        font-size: 1.2rem;
      }
      small {
        position: absolute;
        right: 20px;
        top: -15px;
        font-size: 1rem;
        font-style: italic;
      }
      section.quantity {
        margin: 0;
        input {
          width: 10%;
          border: 1px solid #444;
          border-radius: 3px;
          padding: 10px 0;
          font-size: 1.2rem;
          text-align: center;
          font-weight: bold;
          color: #fff;
          background-color: #444;
          cursor: pointer;
        }
      }
    }
  }
}
</style>
