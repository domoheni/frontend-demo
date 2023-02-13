<template>
  <div class="category">
    <div class="flex-container-column">
      <img :src="category.download_url" alt="" />
      <h4 v-text="category.author"></h4>
      <!-- {{ category.author }} -->
    </div>
  </div>
</template>

<!-- <script setup>
const { data: categories } = await useFetch(
  "https://picsum.photos/v2/list?page=1&limit=10"
);

console.log(categories.value);
const category = categories.value[0];
console.log(category.download_url);
</script> -->

<script>
export default {
  props: {
    category: {
      type: Object,
      default: () => {},
    },
  },
};
</script>
