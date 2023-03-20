<script setup>
import TheHeader from "@/components/TheHeader.vue";
import ProductCard from "@/components/ProductCard.vue";
import { useProductStore } from "./stores/ProductStore";
import { useCartStore } from '@/stores/CartStore';
// import { storeToRefs } from "pinia";
const productStore = useProductStore();
const cartStore = useCartStore()
// const { products } = storeToRefs(useProductStore());  // Only useful when only calling states, not using any actions 

// Calling pinia actions
productStore.fill();
// Use this method or use actions in store directly
// const addToCart = (count, product) => {
//   count = parseInt(count);

  // Using patch function
  // cartStore.$patch((state) => {
  //   for (let index = 0; index < count; index++) {
  //     state.items.push(product);
  //   }
  // });
  // OR
  // for (let index = 0; index < count; index++) {
  //   cartStore.items.push(product);
  // }
// }
</script>

<template>
  <div class="container">
    <TheHeader />
    <ul class="sm:flex flex-wrap lg:flex-nowrap gap-5">
      <ProductCard v-for="product in productStore.products" :key="product.name" :product="product"
        @addToCart="cartStore.addItems($event, product)" />
      <!-- Method1: @addToCart="cartStore.items.push(product)" -->
      <!-- Method2: addToCart($event, product) -->
      <!-- <ProductCard v-for="product in products" :key="product.name" :product="product" /> -->
    </ul>
  </div>
</template>
