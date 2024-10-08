<template>
  <div id="showProductTemplate" class="container text-center mt-3">
    <div class="row">
      <div
        class="p-0 col-md-4"
        v-for="(product, index) in displayedProducts"
        :key="index"
      >
        <div class="card rounded-0">
          <div class="w-100 p-3">
            <img :src="product.img" class="card-img-top w-75" alt="..." />
          </div>
          <div class="card-body">
            <p class="card-text text-start">
              {{ product.title }}
            </p>
          </div>
          <div
            class="card-footer text-body-secondary d-flex justify-content-between align-items-center"
          >
            <a href="#" class="btn btn-outline-success py-0 px-4">
              <i class="bi bi-cart-plus fs-5"></i>
            </a>
            <span id="price" class=""
              >{{ product.price }}<span class="ms-1">تومان</span></span
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, inject, ref } from "vue";
const data = inject("data");
const products = ref(data.products);
const selectedBrands = inject("selectedBrands");
const showAvailable = inject('availabilityStatus')
const displayedProducts = computed(() => {
  let filtered = products.value;
  if (selectedBrands.value.length) {
    filtered = filtered.filter((product) =>
      selectedBrands.value.includes(product.brand.name)
    );
  }
  if (showAvailable.value) {
    filtered = filtered.filter((product) => product.stock > 0);
  }
  return filtered;
});
</script>

<style>
</style>