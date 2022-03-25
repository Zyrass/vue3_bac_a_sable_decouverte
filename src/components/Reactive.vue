<template>
  <h1>Bonjour {{ state.prenom }}</h1>

  <fieldset>
    <legend>{{ state.product.ref }}</legend>
    <h2>{{ state.product.name }}</h2>
    <hr />
    <blockquote>{{ state.product.description }}</blockquote>
    <hr />
    <section class="price">
      <span> <strong>Prix TTC: </strong>{{ prixProductTTC.toFixed(2) }} €</span>
      <span> <strong>Prix HT : </strong>{{ prixProductHT.toFixed(2) }} €</span>
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
  </fieldset>

  <br />

  <section class="quantity">
    <label for="add_product">Combien de formation souhaitez-vous ? </label>
    <input
      type="number"
      min="0"
      :max="state.product.check_quantity"
      v-model="state.product.quantity"
    />
  </section>
</template>

<script setup lang="ts">
import { reactive, ref, computed } from 'vue';

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

<style>
fieldset {
  border: 1px solid #ccc;
  padding: 0 20px 20px;
  margin: 10px;
  margin: 20px 50px;
  max-width: 500px;
  border-radius: 5px;
  box-shadow: 3px 3px 6px #ccc;
  position: relative;
}
blockquote {
  border-left: 5px solid #ccc;
  padding: 10px 20px;
  margin: 10px;
  color: #666;
}
section.price {
  display: flex;
  justify-content: space-between;
  background: #eee;
  padding: 10px;
}
section.price span {
  font-size: 1.2rem;
}
small {
  position: absolute;
  right: 20px;
  top: 0;
  font-size: 0.9rem;
  font-style: italic;
  color: #999;
}

section.quantity {
  margin: 0 0 0 50px;
}
</style>
