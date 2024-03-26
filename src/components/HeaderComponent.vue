<template>
  <header>
    <div
      class="w-full bg-orange-400 h-16 text-center grid items-center justify-items-center"
    >
      <h1 v-text="sitename" class="font-semibold text-2xl text-white"></h1>
    </div>
    <div class="m-4">
      <button
        @click="toggleCheckout"
        class="relative bg-orange-400 text-white px-6 py-4 rounded-md flex items-center justify-center"
      >
        <span
          class="bg-red-500 text-white text-xs font-semibold rounded-full px-2 py-1 absolute -top-2 -right-2"
          >{{ cartItemCount }}</span
        >
        Checkout
      </button>
      <!-- <button
        disabled="disabled"
        class="bg-orange-400 cursor-not-allowed opacity-50 text-white px-6 py-4 rounded-md flex items-center justify-center"
      >
        Checkout
      </button> -->
    </div>
  </header>
</template>

<script>
export default {
  name: "HeaderComponent",
  props: {
    sitename: String,
    cartItemCount: Number,
  },
  methods: {
    toggleCheckout() {
      this.$emit("toggleCheckout");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
