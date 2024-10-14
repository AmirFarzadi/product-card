<template>
  <div id="shoppingCardCpntainer" class=" bg-white position-absolute z-1 rounded shadow p-2">
    <div id="emptyShoppingCart" class=" d-flex justify-content-center flex-column align-items-center pt-4 pb-1" :class="cartList.length!==0 ? 'd-none': 'd-flex'">
      <img src="../assets/cart-empty.svg" alt="" class="w-25 mb-3" />
      <h6 class="text-center">سبد خرید شما خالی است.</h6>
    </div>

    <div id="NoEmptyShoppingCart" class="mx-1" :class="cartList.length !==0 ? 'd-block': 'd-none'">
        <div id="showProductTemplate" :style="cartList.length>2 ? 'height : 370px; overflow-y: scroll' : ''">
            <div id="topSection" class="d-flex justify-content-between py-2">
              <div id="productNumber">
                <span>{{ cart.length.toLocaleString("fa-IR") }} کالا</span>
              </div>
              <div id="closeBtn" class="me-1" @click="showCart ? showCart = false : showCart = true">
                <i class="bi bi-x-lg btn border-0"></i>
              </div>
            </div>
            <div id="productsCartContainer" v-for="(product,index) in cartList" :key="index">
                <div id="productsDetail" class="d-flex gap-2" >
                  <div id="thumbnail" class="w-25 border">
                    <img :src="product.img" alt="" class="w-100 p-1" />
                  </div>
                  <div id="productDescription" class="w-75">
                    <p class="m-0">{{product.title }}</p>
                  </div>
                </div>
                <div class="d-flex justify-content-between align-items-center mt-3">
                  <div class="d-flex">
                      <div id="productNumber" class="border d-flex align-items-center rounded-3">
                        <button class="btn border-0 d-flex justify-content-center align-items-center  px-2 py-1" @click="plusBtnHandler(product.id)">
                            <i class="bi bi-plus-lg text-primary"></i>
                        </button>
                        <span class="px-2 text-primary">{{ product.qty }}</span>
                        <button class="btn border-0 d-flex justify-content-center align-items-center px-2 py-1" @click="minusBtnHandler(product.id)">
                            <i class="bi bi-dash-lg text-primary"></i>
                        </button>
                    </div>
          
          
                    <div id="delletProductBtn" class="bg-danger ms-3 px-2 py-1 rounded d-flex align-items-center justify-content-center" @click="deleteProductFromCart(product.id)">
                      <i class="bi bi-trash text-white"></i>
                    </div>
                  </div>
          
                    <div id="productPrice" class="d-flex">
                      <span id="price" class="iranyekan_ebold"
                        >{{ Number(product.price * product.qty).toLocaleString("fa-IR")
                        }}<span class="ms-1">تومان</span>
                    </span>
                    </div>
                </div>
                <hr class="text-muted">
            </div>
        </div>

      <div id="allProductsDetail" class="d-flex justify-content-between align-items-center">
          <div id="totalPriceDetails" class="ms-3">
            <div class="d-flex flex-column gap-3">
              <span>مبلغ قابل پرداخت</span>
              <span id="price" class="iranyekan_ebold text-danger"
              >{{ Number(totalPrice).toLocaleString("fa-IR")
              }}<span class="ms-1">تومان</span></span>
            </div>
          </div>
        <div id="orderRegistration" class="me-3">
            <button class="btn btn-danger">ثبت سفارش</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { inject, ref, watch } from "vue";
import Swal from 'sweetalert2'

const cart = inject('cart')
const deleteBtn = inject('deleteBtn')
const cartList = ref([])
const showCart = inject('showCart')
const totalPrice = ref(0)


watch(()=>cart.value,(newval)=>{
    cartList.value = newval
    calculateTotalPrice()
},{deep:true,immediate:true})

function deleteProductFromCart(id){
    deleteBtn(id)
}

function plusBtnHandler(id){
    const item = cart.value.find(element => element.id == id);  
    if (item) {  
        item.qty += 1
        if(item.qty > item.stock){
            item.qty = item.stock
            Swal.fire({
                position: "top-start",
                icon:'warning',
                text: `فقط ${item.stock.toLocaleString("fa-IR")} عدد از محصول در انبار موجود است.`,
                showConfirmButton: false,
                timer: 1500
            });
        }
    }  
}
function minusBtnHandler(id){
    const item = cart.value.find(element => element.id == id);  
    if (item) {  
        item.qty -= 1; 
        if (item.qty < 1) {  
            item.qty = 1;
        }  
    }  
}

function calculateTotalPrice() {  
    let total = 0; 
    cart.value.forEach(element => {  
        total += (element.qty * element.price);
    });  
    totalPrice.value = total;
}

// function wareHouseStock(){

// }
</script>

<style>
#shoppingCardCpntainer {
  position: relative;
  left: 225px;
  top: 55px;
  width: 400px;
  height: auto;
}
#shoppingCardCpntainer::after {
  content: "";
  width: 0;
  height: 0;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-bottom: 10px solid white;
  position: absolute;
  top: -10px;
  left: -3px;
  left: 18px;
}
</style>