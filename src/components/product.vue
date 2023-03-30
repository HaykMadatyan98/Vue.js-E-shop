<script>
export default {
  name: "Product",
  props: ["product", "addInBasketFtn"],

  data() {
    return {
      count: 0,
    };
  },
  methods: {
    handleAddInBasket() {
      this.addInBasketFtn(this.product.id, this.count);
      this.count = 0;
    },
  },
};
</script>

<template>
  <div
    class="flex justify-between items-center w-2/5 rounded-2xl border-2 border-black p-4"
  >
    <div class="text-center w-20">
      <img :src="product.photo" class="w-20 h-20" />
      <span class="w-10">{{ product.name }}</span>
    </div>

    <div class="flex flex-col text-center w-10">
      <span>Price:</span>
      <span class="w-10">{{ product.price }}</span>
    </div>

    <div class="flex text-center w-20">
      <span>Count:</span>
      <input v-model="count" type="number" min="0" class="w-12 text-center" />
    </div>

    <div
      class="flex text-center w-32"
      :class="product.price * count > 100000 ? 'flex-col' : 'flex-row'"
    >
      <span>Total Price: </span>
      <span>{{ product.price * count }}</span>
    </div>

    <button
      @click="handleAddInBasket"
      class="w-1/5 rounded-2xl border-2 border-black"
    >
      Add to basket
    </button>
  </div>
</template>

<style></style>
