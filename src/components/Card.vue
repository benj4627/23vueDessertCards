<script setup>
//imports
import { ref } from 'vue';
import jsonData from '../assets/data/data.json'

const props = defineProps(['addToBasket'])
const data = ref(jsonData)
</script>

<template>
 <main>
    <h2 class="titleDessert">Desserts</h2>
    <section class="cardContainer">
        <article class="card" 
        v-for="product in data" 
        :key="product.name">
            <img :src="product.image.desktop" :alt="product.name"
            :class="{ activeCard: product.quantity > 0 }">
            
                <el-button v-if="!product.quantity"
                class="addToCartBtn" 
                type="primary" 
                plain round color="#4e54c9"
                @click="addToBasket(product)"
                >
                    <i class="fa-solid fa-cart-shopping"></i>Add to Cart
                </el-button>    
           
            <h3 class="category">{{ product.category }}</h3>
            <h3 class="title">{{ product.name }}</h3>
            <h3 class="price">${{ product.price }}</h3>
        </article>
    </section>

  </main>
</template>

<style>
.inputNumber {
    width: 100%;
    color: #4e54c9
}
h2 {
    max-width: 1320px;
    margin: 0 auto;
    font-size: 3rem;
    font-weight: bold;
    color: #4e54c9;
    padding: 1rem 0;
    letter-spacing: .3rem;
}

.titleDessert {
    letter-spacing: 1rem;
    font-size: 6rem;
    font-weight: 1000;
}

.addToCartBtn {
    transition: .3s ease-in-out;
    font-weight: 700;
    letter-spacing: .1rem;
    border: 2px solid #4e54c9;
}

.cardContainer {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(290px, 1fr));
    gap: 2rem;
}

.card {
    border-radius: 20px;
    width: 80%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 0.5rem;
    transition: .3s ease-in-out;
}

.card i {
    margin-right: .5rem;
}

.price {
    font-weight: bold;
    color: #4e54c9;
    font-size: 1.1rem;
}

.category {
    color: rgb(119, 119, 119);
    font-size: 0.9rem;
}

.title {
    font-size: 1.1rem;
    font-weight: 700;
}

img {
    border-radius: 15px;
    border: 2px solid rgba(0, 0, 0, 0);
    transition: .3s ease-in-out;
}

.inputNumber .el-input__inner {
    color: #4e54c9;
    border-color: #4e54c9; 
}

.activeCard {
    border: 2px solid #4e54c9;
}

</style>