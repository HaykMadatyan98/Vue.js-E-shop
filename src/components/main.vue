<script>
import Product from "./product.vue";

export default {
  name: "Main",
  props: ["products", "addInBasketFtn"],
  components: {
    Product,
  },

  data() {
    return {};
  },
};
</script>

<template>
  <div class="flex flex-col items-center gap-5">
    <Product
      v-for="item in products"
      :product="item"
      :addInBasketFtn="addInBasketFtn"
    />
  </div>
</template>

<style></style>
