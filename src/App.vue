<template>
  <NavbarSection/>

  <div id="filterBox" class="container mt-3 mb-3 border p-3 d-flex justify-content-between">
    <div id="rightBox" class="d-flex align-items-center justify-content-start">
      <FilterBrand :data="'brands'"/>
      <AvailableProduct @updateAvailabilityFilter="updateAvailabilityStatus"/>
      <FilterBtn/>
    </div>
    <div id="leftBox" class="d-flex align-items-center">
      <SortProducts @updateSort = "updateSortProduct" />
    </div>
  </div>

  <div id="productsNumber" class="container d-flex justify-content-end">
    <span class="justify-content-end">{{ data.products.length }}کالا</span>
  </div>

  <ShowProductTemplate/>
</template>

<script setup>  
import {  provide, ref  } from "vue";  
//components
import FilterBrand from "./components/FilterSection/FilterBrand.vue";
import ShowProductTemplate from "./components/ShowProductTemplate.vue";
import AvailableProduct from "./components/FilterSection/AvailableProduct.vue";
import NavbarSection from "./components/NavbarSection/NavbarSection.vue";
import FilterBtn from "./components/FilterSection/FilterBtn.vue";
import SortProducts from "./components/FilterSection/SortProducts.vue"
//components
import data from "./data.json";  
provide("data",data)
const selectedBrands = ref([]);  
provide('selectedBrands', selectedBrands); 


const availabilityStatus = ref(null)
provide('availabilityStatus',availabilityStatus)
function updateAvailabilityStatus (index){
  availabilityStatus.value = index
}


const sortUpdated = ref(null)
provide('sortUpdated',sortUpdated)
function updateSortProduct (index){
  sortUpdated.value = index
}


// const number = ref(12300000)
// console.log(number.value.toLocaleString('fa-IR'));
</script>

<style>
body{
  padding-bottom: 500px;
}
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
