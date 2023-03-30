<script>
import Main from "./components/main.vue";
import Basket from "./components/basket.vue";

export default {
  name: "App",

  components: {
    Main,
    Basket,
  },

  data() {
    return {
      products: [
        {
          id: 0,
          name: "Apple",
          price: 500,
          photo:
            "https://media.istockphoto.com/id/184276818/photo/red-apple.jpg?s=612x612&w=0&k=20&c=NvO-bLsG0DJ_7Ii8SSVoKLurzjmV0Qi4eGfn6nW3l5w=",
        },
        {
          id: 1,
          name: "Orange",
          price: 700,
          photo:
            "https://thumbs.dreamstime.com/b/sliced-orange-fruit-leaves-isolated-white-23331258.jpg",
        },
        {
          id: 2,
          name: "Kiwi",
          price: 300,
          photo:
            "https://www.naturespride.eu/media/fzxfw2x4/kiwi-productfoto-hayward-vari%C3%ABteit.jpg?anchor=center&mode=crop&width=1000&height=1000&rnd=132457563923470000",
        },
        {
          id: 3,
          name: "Grenade",
          price: 500,
          photo:
            "https://media.istockphoto.com/id/940118920/photo/ripe-pomegranate-fruit-and-one-cut-in-half-with-leaf.jpg?s=612x612&w=0&k=20&c=iVTrJvW6rtFTlsWk5J3v1r1NeCgNtZMD4qDJIh3sfik=",
        },
      ],
      productsInBasket: [],
      isHomePage: true,
    };
  },
  computed: {
    calcSum() {
      return this.productsInBasket.reduce(
        (acc, item) => acc + item.price * item.count,
        0
      );
    },
  },
  methods: {
    addInBasketFtn(id, count = 1) {
      if (this.productsInBasket.findIndex((item) => item.id === id) > -1) {
        this.productsInBasket.forEach((item) => {
          item.count = item.id === id ? count + item.count : item.count;
        });
      } else if (count > 0) {
        this.productsInBasket.push({
          ...this.products[id],
          count,
        });
      }
    },
    incressProduct(id) {
      this.productsInBasket = this.productsInBasket
        .map((item) => {
          item.count = item.id === id ? item.count - 1 : item.count;
          return item;
        })
        .filter((item) => item.count !== 0);
    },
    deleteProduct(id) {
      this.productsInBasket = this.productsInBasket.filter(
        (item) => item.id !== id
      );
    },
    payFtn() {
      if (this.productsInBasket.length) {
        alert("Thanks for pay");
      } else {
        alert("Please add items to basket");
      }
      this.productsInBasket = [];
    },
  },
};
</script>

<template>
  <div class="flex justify-between h-40 m-5 mx-96">
    <span @click="isHomePage = true" class="cursor-pointer">Home</span>
    <span @click="isHomePage = false" class="cursor-pointer">
      Basket: {{ productsInBasket.length }} - {{ calcSum }}$
    </span>
  </div>
  <Main
    v-if="isHomePage"
    :products="products"
    :addInBasketFtn="addInBasketFtn"
  />
  <Basket
    v-else
    :productsInBasket="productsInBasket"
    :totalPrice="calcSum"
    :payFtn="payFtn"
    :deleteProduct="deleteProduct"
  />
</template>

<style>
.header {
  display: flex;
  justify-content: space-between;
  height: 200px;
  margin: 20px;
}
</style>
