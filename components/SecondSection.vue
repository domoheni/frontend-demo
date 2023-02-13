<template>
  <section class="text-image">
    <div class="container">
      <h2>Cím</h2>
      <div class="split-text">
        <div class="item1">
          <p v-for="b in bacons" v-text="b"></p>
        </div>
        <div class="item2">
          <img src="/images/cover-photo.png" alt="" />
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    bacons: {
      type: Object,
      default: () => {},
    },
  },
};
</script>
