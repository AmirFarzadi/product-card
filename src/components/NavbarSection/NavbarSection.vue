<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
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
        <i class="bi bi-person-fill fs-4 btn border-0 p-0"></i>
        <span class="line mx-3 mt-2"></span>
        <i class="bi bi-cart-fill fs-4 btn border-0 p-0" @click="cartBtnHandler"></i>
      </div>
    </div>
  </nav>
  <shoppingCart v-if="showCart"/>
</template>

<script setup>
import { provide, ref } from 'vue';
import shoppingCart from '../shoppingCart.vue';
const showCart = ref(false)
provide('showCart', showCart)
function cartBtnHandler(){
  showCart.value ? showCart.value = false : showCart.value = true
}
</script>

<style>
</style>