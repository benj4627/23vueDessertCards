<script setup>
import { computed, ref } from 'vue';

let props = defineProps(['basketItems', 'removeFromBasket']);

//Calculates order total using computed
let orderTotal = computed(() => {
  return props.basketItems.reduce((total, item) => total + (item.price * item.quantity), 0);
});

//Modal visibility state + function to handle button click
let showModal = ref(false);
let showModalConfirm = () => {
    showModal.value = true;
}

</script>

<template>
    <article class="basketContainer">
      <h2>Your Cart ({{ basketItems.length }})</h2>
  
      <div v-for="item in basketItems" :key="item.name" class="basketContentContainer">
        <div class="basketItem">
          <h3>{{ item.name }}</h3>
          <div class="itemDetails">
            <p>{{ item.quantity }}x</p>
            <p>@ ${{ item.price }} -</p>
            <p>${{ (item.price * item.quantity).toFixed(2) }}</p>
          </div>
        </div>
  
        <div class="flexContainerInputCross">
            <el-input-number 
                v-model="item.quantity"
                :min="0"
                :max="10000"
                size="small"
                />
                <div class="basketCross" @click="removeFromBasket(item)">
                <i class="fa-regular fa-circle-xmark"></i>
                </div>
        </div>
      </div>

        <div class="orderTotal">
            <h4>Order Total</h4>
            <transition name="fade" mode="out-in">
                <p :key="orderTotal">$ {{ orderTotal }}</p>
            </transition>
        </div>
      <el-button class="addToCartBtn confirmBtn" type="primary" plain round color="#4e54c9" @click="showModalConfirm">Confirm Order</el-button>

      <!-- modal -->
      <transition name="fade">
        <div v-if="showModal" class="modalBackdrop" @click="showModal = false">
        <div class="modalContent" @click.stop>
            <h2 class="titleModal">Thank you so much for your order!</h2>
            <p class="descpModal">Our team is currently putting your order in the oven! You'll receive an email when it's ready for pickup!</p>
            <el-button class="addToCartBtn confirmBtn modalBtn" type="primary" plain round color="#4e54c9" @click="showModal = false">
            Great! Close this box
            </el-button>
        </div>
        </div>
  </transition>
    </article>
  </template>

<style scoped>  

  .modalContent {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 3;
    background-color:  #fffbfb;
    border-radius: 20px;
    height: 55vh;
    width: 40vw;
    padding: 4rem;
    transition: .3s ease-in-out;
  }

  .descpModal {
    font-size: 1.3rem;
    line-height: 120%;
    margin-top: 2rem;
  }

  .modalBackdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.659); 
    box-shadow: 0 0 150px rgba(0, 0, 0, 0.7);
    z-index: 4;
}

 .basketContainer {
    background-color: rgb(255, 252, 252);
    padding: 2rem;
    width: fit-content;
    border-radius: 15px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1), 0 1px 3px rgba(0, 0, 0, 0.08);
}

.basketTitle {
    font-size: 1.3rem;
    font-weight: bold;
    margin-bottom: 1rem;
    color: #4e54c9;
}

.basketContentContainer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid #ddd;
    padding: 0.5rem 0;
}

.basketItem {
    display: flex;
    flex-direction: column;
}

.basketItem h3 {
    font-weight: bold;
}

.itemTitle {
    font-size: 1rem;
    font-weight: bold;
    color: #333;
}

.itemDetails {
    display: flex;
    gap: 0.3rem;
    align-items: center;
    justify-content: flex-start;
    font-size: 0.9rem;
    color: #666;
}

.numberOfItems {
    color: #4e54c9;
    font-weight: bold;
}

.itemPrice,
.itemTotal {
    color: #666;
}

.basketCross {
    cursor: pointer;
    color: #888;
}

.basketCross i {
    font-size: 1rem;
    transition: .3s ease-in-out;
    margin-bottom: 2.5rem;
    margin-top: .3rem;
}

.basketCross i:hover {
    color: #4e54c9;
    transform: scale(110%);
}

.confirmBtn {
    width: 100%;
    padding: 1rem 2rem;
    margin-top: 2rem;
}

.basketContainer h2 {
    font-size: 2rem;
    font-weight: bold;
    color: #4e54c9;
    padding: 1rem 0;
}

.flexContainerInputCross {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    gap: .5rem
}

.orderTotal {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 2rem;
}

.orderTotal h4 {
    font-size: 2rem;
    font-weight: bold;

}

.orderTotal p {
    margin: unset;
    color: #4e54c9;
    font-weight: bold;
    font-size: 1.5rem
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease-in-out;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

.modalBackdrop.fade-enter-active, .modalContent.fade-enter-active {
  opacity: 1;
}

.modalBackdrop.fade-leave-active, .modalContent.fade-leave-active {
  opacity: 0;
}
</style>