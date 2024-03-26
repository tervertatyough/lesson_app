<template>
  <div>
    <div>
      <checkout-card
        :cart="cart"
        :get-lesson-details="getLessonDetails"
        @remove-lesson="removeFromCart"
      ></checkout-card>
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
  methods: {
    removeFromCart(lessonId) {
      this.$emit("removeLesson", lessonId);
    },
  },
};
</script>
