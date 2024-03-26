<template>
  <div class="flex flex-wrap w-full">
    <div
      v-for="(lessonId, index) in cart"
      :key="index"
      class="bg-orange-400 w-70 p-4 m-2 flex flex-col items-center"
    >
      <div v-if="getLessonDetails(lessonId)">
        <figure>
          <img class="h-48" :src="getLessonDetails(lessonId).image" alt="" />
        </figure>
        <div class="items-start my-4">
          <h3>
            Lesson:
            <span class="font-semibold text-base">{{
              getLessonDetails(lessonId).programme
            }}</span>
          </h3>
          <p>
            Location:
            <span class="font-semibold text-base">{{
              getLessonDetails(lessonId).location
            }}</span>
          </p>
          <p>
            Price:
            <span class="font-semibold text-base">{{
              getLessonDetails(lessonId).price
            }}</span>
          </p>
        </div>
        <button
          @click="removeFromCart(lessonId)"
          class="bg-white text-orange-400 hover:bg-gray-300 font-bold py-2 px-4 my-2 w-full rounded"
        >
          Remove
        </button>
      </div>
      <div v-else>
        <p>Lesson details not found for ID: {{ lessonId }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CheckoutCard",

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

<style scoped></style>
