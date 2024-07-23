<script setup>
import axios from "axios";
import { reactive, onMounted } from "vue";
import { useRoute, RouterLink } from "vue-router";

const state = reactive({
  products: [],
  isLoading: true,
});

onMounted(async () => {
  try {
    const response = await axios.get("https://fakestoreapi.com/products");
    state.products = response.data;
    console.log(state.products);
  } catch (error) {
    console.error("Error taking the Fakestore API", error);
  } finally {
    state.isLoading = false;
  }
});
</script>

<template>
  <div class="mx-auto w-[80%] py-5 grid grid-cols-3">
    <div v-for="product in state.products" :key="product.id" class="max-w-sm bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700 mb-4 items-center justify-center flex flex-col">
      <RouterLink to="#">
        <img class="rounded-t-lg w-32 h-32 object-cover object-center" :src="product.image" alt="Product Images" />
      </RouterLink>
      <div class="p-5">
        <RouterLink to="#">
          <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">{{ product.title }}</h5>
        </RouterLink>
        <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">{{ product.description }}</p>
        <RouterLink
          to="#"
          class="inline-flex items-center px-3 py-2 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
        >
          Read more
          <svg class="rtl:rotate-180 w-3.5 h-3.5 ms-2" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 14 10">
            <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 5h12m0 0L9 1m4 4L9 9" />
          </svg>
        </RouterLink>
      </div>
    </div>
  </div>
</template>
