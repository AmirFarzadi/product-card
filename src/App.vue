<template>
  <nav
   class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container position-relative">
      <a class="navbar-brand d-none d-lg-block" href="#">
        <!-- <img src="/docs/5.3/assets/brand/bootstrap-logo.svg" alt="Bootstrap" width="30" height="24"> -->
        Navbar</a
      >
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#"
              >صفحه اصلی</a
            >
          </li>
          <li class="nav-item">
            <a class="nav-link text-danger" href="#">شگفت انگیزها</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">درباره ما</a>
          </li>
          <li class="nav-item">
            <a class="nav-link">تماس باما</a>
          </li>
        </ul>
      </div>
      <div class="d-flex position-absolute icons">
        <i class="bi bi-person-fill fs-4"></i>
        <span class="line mx-3 mt-2"></span>
        <i class="bi bi-cart-fill fs-4"></i>
      </div>
    </div>
  </nav>

  <div
    id="filterBox"
    class="container mt-3 mb-3 border p-3 d-flex justify-content-between"
  >
    <div id="rightBox" class="d-flex align-items-center justify-content-start">
      <FilterBrand :data="'brands'"/>
      <div class="form-check form-switch me-3">
        <input
          class="form-check-input"
          type="checkbox"
          role="switch"
          id="flexSwitchCheckDefault"
        />
        <label class="form-check-label text-muted" for="flexSwitchCheckDefault"
          >فقط کالاهای موجود</label
        >
      </div>

      <button type="button" class="btn btn-primary btn-sm">
        <i class="bi bi-funnel-fill"></i>
        اعمال فیلتر
      </button>
    </div>
    <div id="leftBox" class="d-flex align-items-center">
      <i class="bi bi-sort-down me-2 fs-5"></i>
      <select class="form-select-sm" aria-label="Default select example">
        <option selected>مرتب سازی</option>
        <option value="newest">جدیدترین</option>
        <option value="oldest">قدیمی ترین</option>
        <option value="mostExpensive">گرانترین</option>
        <option value="cheapest">ارزانترین</option>
        <option value="bestSeller">پرفروش ترین</option>
      </select>
    </div>
  </div>

  <div id="productsNumber" class="container d-flex justify-content-end">
    <span class="justify-content-end">{{ data.products.length }}کالا</span>
  </div>

  <div id="showProductTemplate" class="container text-center mt-3">
    <div class="row">
      <div
        class="p-0 col-md-4"
        v-for="(product, index) in filteredProducts"
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
import {  provide , computed , ref} from "vue";  
import FilterBrand from "./components/FilterBrand.vue";
import data from "./data.json";  
provide("data",data)
// Variables  
const products = ref(data.products);  
const selectedBrands = ref([]);  

const filteredProducts = computed(() => {  
  if (selectedBrands.value.length) {  
    return products.value.filter(product => selectedBrands.value.includes(product.brand.name));  
  }  
  return products.value;   
});  
provide("selectedBrands",selectedBrands)
</script>

<style>
.line {
  width: 2px;
  background-color: rgb(136, 134, 134);
  height: 20px;
  display: block;
}
.icons {
  left: 0;
  top: 5px;
}
#brand-dropdown {
  text-decoration: none;
}
#brand-dropdown:hover {
  color: black !important;
}
</style>
