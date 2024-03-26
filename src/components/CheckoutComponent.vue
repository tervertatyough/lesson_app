<template>
  <div>
    <div>
      <checkout-card
        :cart="cart"
        :get-lesson-details="getLessonDetails"
        @remove-lesson="removeFromCart"
      ></checkout-card>
    </div>
    <div v-if="!orderPlaced" class="m-4 flex flex-col items-center">
      <input
        type="text"
        v-model="order.name"
        placeholder="Enter your name"
        class="border p-2 rounded-md mb-2"
      />
      <input
        type="text"
        v-model="order.number"
        placeholder="Enter your phone number"
        class="border p-2 rounded-md mb-2"
      />
      <button
        @click="placeOrder"
        :disabled="!canPlaceOrder"
        class="bg-blue-500 text-white px-4 py-2 rounded-md"
      >
        Place Order
      </button>
    </div>
    <div v-else class="m-4">
      <h2 class="text-xl font-semibold">Order Placed Successfully!</h2>
      <p class="font-semibold">Name: {{ order.name }}</p>
      <p class="font-semibold">Phone Number: {{ order.number }}</p>
      <!-- Additional order details can be displayed here -->
    </div>
  </div>
</template>

<script>
import CheckoutCard from "./CheckoutCard.vue";

export default {
  components: { CheckoutCard },
  name: "CheckoutComponent",
  props: {
    cart: {
      type: Array,
      required: true,
    },
    getLessonDetails: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      order: {
        name: "",
        number: "",
      },
      orderPlaced: false,
    };
  },
  computed: {
    canPlaceOrder() {
      return this.order.name.trim() !== "" && this.order.number.trim() !== "";
    },
  },
  methods: {
    removeFromCart(lessonId) {
      this.$emit("removeLesson", lessonId);
    },
    placeOrder() {
      this.orderPlaced = true;
    },
  },
};
</script>
