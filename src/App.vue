<template>
  <div class="mx-12">
    <HeaderComponent
      sitename="M00961778 Coursework 3"
      :cartItemCount="cartItemCount"
      @toggleCheckout="toggleCheckout"
    />
    <div v-if="!showCheckout || cart.length <= 0">
      <div class="flex flex-wrap w-full">
        <LessonCard
          v-for="lesson in lessons"
          :key="lesson.id"
          :lesson="lesson"
          @addLesson="addToCart"
          :cart="cart"
        />
      </div>
    </div>
    <div v-if="showCheckout">
      <checkout-component
        :cart="cart"
        :get-lesson-details="getLessonDetails"
        @removeLesson="removeFromCart"
      ></checkout-component>
    </div>
  </div>
</template>

<script>
import HeaderComponent from "./components/HeaderComponent.vue";
import LessonCard from "./components/LessonCard.vue";
import CheckoutComponent from "./components/CheckoutComponent.vue";

export default {
  name: "App",
  components: {
    HeaderComponent,
    LessonCard,
    CheckoutComponent,
  },
  data() {
    return {
      lessons: [],
      cart: [],
      showCheckout: false,
    };
  },
  computed: {
    cartItemCount() {
      return this.cart.length;
    },
  },
  mounted() {
    this.fetchLessons();
  },
  methods: {
    addToCart(lesson) {
      this.cart.push(lesson._id);
    },
    toggleCheckout() {
      this.showCheckout = !this.showCheckout;
    },
    fetchLessons() {
      // Fetch lessons from the server
      fetch(
        "http://products-env.eba-gpri3t2b.eu-north-1.elasticbeanstalk.com/collection/products",
        {
          method: "GET",
          headers: {
            "Content-Type": "application/json",
          },
        }
      )
        .then((response) => response.json())
        .then((responseJSON) => {
          // Update the lessons data with the fetched lessons
          this.lessons = responseJSON;
        })
        .catch((error) => {
          console.error("Error fetching lessons:", error);
        });
    },
    removeFromCart(lesson) {
      // Find the index of the lesson in the cart
      const index = this.cart.findIndex((item) => item._id === lesson._id);
      // If the lesson is found, remove it from the cart
      if (index !== -1) {
        this.cart.splice(index, 1);
      }
    },

    getLessonDetails(lessonId) {
      // Find the lesson with the given lessonId
      return this.lessons.find((lesson) => lesson._id === lessonId);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
