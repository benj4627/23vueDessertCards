<script setup>
import { ref } from 'vue';
import Card from './components/Card.vue';
import Basket from './components/Basket.vue';

const basketItems = ref([]);

/// Function to add items to the basket
const addToBasket = (product) => {
  const existingItem = basketItems.value.find((item) => item.name === product.name);
  
  // If product already exists, increment the quantity
  if (existingItem) {
    existingItem.quantity += 1;
  } else {
    
    basketItems.value.push({ ...product, quantity: 1 });
  }
};

// Function to remove products from the basket
const removeFromBasket = (product) => {
  // Filter out the product by its name
  basketItems.value = basketItems.value.filter((item) => item.name !== product.name);
};


</script>

<template>
  <header></header>

  <main>
    <div class="gridContainer">
      <section class="cards">
        <Card :addToBasket="addToBasket" />
      </section>
      
      <div class="basketContainer">
        <transition name="fade">
          <div>
            <Basket :basketItems="basketItems" :removeFromBasket="removeFromBasket" />
          </div>
        </transition>
      </div>
    </div>
  </main>

  <footer></footer>
</template>

<style scoped>
main {
  max-width: 1300px;
  margin: 0 auto;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

.gridContainer {
  display: grid;
  grid-template-columns: 6fr 1fr;
  align-items: start;
}

.basketContainer {
  margin-top: 5.2rem;
  width: 350px;
}

</style>
