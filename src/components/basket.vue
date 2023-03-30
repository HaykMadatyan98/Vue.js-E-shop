<script>
import Form from "./form.vue";

export default {
  name: "Basket",
  props: ["productsInBasket", "totalPrice", "payFtn", "deleteProduct"],
  components: {
    Form,
  },
  data() {
    return {};
  },
};
</script>

<template>
  <div class="flex justify-center align-center">
    <div class="w-1/3 flex flex-col gap-4">
      <span>Total price: {{ totalPrice }}</span>
      <div class="flex justify-start flex-col">
        <div
          v-for="product in productsInBasket"
          class="flex justify-start gap-4 items-center"
        >
          <img :src="product.photo" class="w-20 h-20" />
          <span>Name: {{ product.name }}</span>
          <span>
            Count:
            <input
              v-model="product.count"
              type="number"
              min="1"
              class="w-12 text-center"
            />
          </span>
          <span>Price: {{ product.price }}</span>
          <span>Total Price: {{ product.price * product.count }}</span>
          <span
            class="flex border-2 border-black w-5 h-5 items-center justify-center cursor-pointer rounded-full"
            @click="deleteProduct(product.id)"
            >X</span
          >
        </div>
      </div>
    </div>
    <Form :payFtn="payFtn" class="w-1/3 border-l-2 border-black" />
  </div>
</template>

<style></style>
