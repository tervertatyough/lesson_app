<template>
  <div class="bg-orange-400 w-70 p-4 m-2 flex flex-col items-center">
    <figure>
      <img class="h-48" :src="lesson.image" alt="" />
    </figure>
    <div class="items-start my-4">
      <h3>
        Lesson:
        <span class="font-semibold text-base">{{ lesson.programme }}</span>
      </h3>
      <p>
        Location:
        <span class="font-semibold text-base"> {{ lesson.location }}</span>
      </p>
      <p>
        Price:
        <span class="font-semibold text-base">{{ lesson.price }}</span>
      </p>
      <p>
        Spaces Available:
        <span class="font-semibold text-base"
          >{{ lesson.spaces - cartCount(lesson._id) }}
        </span>
      </p>
    </div>
    <button
      @click="addToCart(lesson)"
      class="bg-white text-orange-400 hover:bg-gray-300 font-bold py-2 px-4 my-2 w-full rounded"
    >
      Add To Cart
    </button>
  </div>
</template>

<script>
export default {
  name: "LessonCard",
  props: {
    lesson: {
      type: Object,
      required: true,
    },
    cart: {
      type: Array,
      required: true,
    },
  },
  methods: {
    addToCart(lesson) {
      this.$emit("addLesson", lesson);
    },

    cartCount(id) {
      let count = 0;
      for (let i = 0; i < this.cart.length; i++) {
        if (this.cart[i] === id) {
          count++;
        }
      }
      return count++;
    },
  },
};
</script>

<style scoped></style>
