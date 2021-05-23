<template>
  <div class="columns is-multiline is-centered">
    <div
      v-for="product in products"
      :key="product.id"
      class="column is-one-quarter card m-2"
    >
      <div class="card-image">
        <figure class="image is-4by3">
          <img
            src="https://bulma.io/images/placeholders/640x480.png"
            alt="Placeholder image"
          />
        </figure>
      </div>
      <div class="card-content">
        {{ product.title }} - {{ currency(product.price) }}
        <br />
        <button
          :disabled="!product.inventory"
          @click="addProductToCart(product)"
          class="button is-primary"
        >
          Add to cart
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { computed } from "vue";
import { useStore } from "vuex";
import { currency } from "../helpers/currency";
export default {
  setup() {
    const store = useStore();
    const products = computed(() => store.state.products.all);
    const addProductToCart = (product) =>
      store.dispatch("cart/addProductToCart", product);
    store.dispatch("products/getAllProducts");
    return {
      products,
      addProductToCart,
      currency,
    };
  },
  // computed: mapState({
  //   products: state => state.products.all
  // }),
  // methods: mapActions('cart', [
  //   'addProductToCart'
  // ]),
  // created () {
  //   this.$store.dispatch('products/getAllProducts')
  // }
};
</script>
<style>
.card {
}
</style>