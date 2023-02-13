<template>
  <header class="navbar">
    <div class="container">
      <Navbar />
    </div>
  </header>
  <FirstSection />
  <SecondSection :bacons="bacons" />

  <section class="categories">
    <div class="container">
      <div class="flex-container-column">
        <h2>Képek</h2>
        <button
          @click="next()"
          v-if="page < limit"
          v-text="'Következő: ' + page"
        ></button>
        <div class="categories">
          <Category
            v-for="category in categories"
            :category="category"
            :key="category.id"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, watch } from "vue";
// PAGE HEAD
useHead({
  title: "MyITSolver",
});

// BACONIPSUM
const { data: bacon } = await useFetch(
  "https://baconipsum.com/api/?type=all-meat&paras=2&start-with-lorem=1"
);
const bacons = bacon.value;
const router = useRouter();
const route = useRoute();
const routNumb = Number(route.params.number);
const search = ref("");
const page = ref(routNumb);
const limit = 10;

const { data: categories, error } = await useAsyncData(
  "categories",
  () =>
    $fetch(`/v2/list?page=?&limit=10`, {
      method: "GET",
      baseURL: "https://picsum.photos",
      params: {
        page: page.value,
        search: search.value,
      },
    }),
  {
    watch: [page, search],
  }
);

function setQuery() {
  router.push({ params: { number: page.value } });
}

const next = () => {
  if (page.value + 1 <= limit) {
    page.value = page.value + 1;
    setQuery();
  }
};
</script>
