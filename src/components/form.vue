<script>
export default {
  name: "Form",
  props: ["payFtn"],
  data() {
    return {
      email: null,
      cardNumber: null,
      date: null,
      cvc: null,
      name: null,
      valid: false,
    };
  },
  methods: {
    handlePay() {
      if (this.checkIsValid) {
        this.payFtn();
      } else {
        alert("Form is not valid");
      }
    },
  },
  computed: {
    checkEmail() {
      return this.email?.includes("@");
    },
    checkCardNumber() {
      return this.cardNumber?.length === 16;
    },
    checkCardDate() {
      return this.date?.length === 5 && this.date[2] === "/";
    },
    checkCVCNumber() {
      return this.cvc?.length === 3;
    },
    checkName() {
      return this.name?.includes("") && this.name?.length > 3;
    },
    checkIsValid() {
      return (
        this.checkEmail &&
        this.checkCardNumber &&
        this.checkCardDate &&
        this.checkCVCNumber &&
        this.checkName
      );
    },
  },
};
</script>

<template>
  <div
    class="flex flex-col form w-2/5 h-full pt-20 justify-between items-center gap-16"
  >
    <div class="flex flex-col w-4/5">
      <input
        v-model="email"
        class="w-full"
        placeholder="Email"
        :class="checkEmail ? 'valid' : 'notValid'"
      />
    </div>
    <div class="flex flex-col w-4/5 gap-2">
      <span>Card information</span>
      <input
        v-model="cardNumber"
        placeholder="1234 1234 1234 1234"
        forma
        class="w-full"
        :class="checkCardNumber ? 'valid' : 'notValid'"
      />
      <div>
        <input
          v-model="date"
          placeholder="MM/YY"
          class="w-1/2"
          :class="checkCardDate ? 'valid' : 'notValid'"
        />
        <input
          v-model="cvc"
          placeholder="CVC"
          class="w-1/2"
          :class="checkCVCNumber ? 'valid' : 'notValid'"
        />
      </div>
    </div>
    <div class="w-4/5">
      <input
        v-model="name"
        class="w-full"
        placeholder="Name on card"
        :class="checkName ? 'valid' : 'notValid'"
      />
    </div>
    <button
      class="w-1/5 rounded-2xl h-10 border-2 border-black text-center"
      :class="isValid ? 'valid' : 'notValid'"
      @click="handlePay"
    >
      Pay
    </button>
  </div>
</template>

<style>
.form input {
  height: 50px;
  padding-left: 15px;
  border-radius: 20px;
}

button:hover {
  background-color: gray;
  color: white;
}

.valid {
  border: 1px solid green;
}

.notValid {
  border: 1px solid red;
}
</style>
