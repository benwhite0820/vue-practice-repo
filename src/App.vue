<script setup>
import { ref } from 'vue';
import socksGreenImage from './assets/socks_green.jpeg';
import socksBlueImage from './assets/socks_blue.jpeg';

const product = ref('Socks');
const image = ref(socksGreenImage);
const inStock = ref(false);

const details = ref(['50% cotton', '30% wool', '20% polyester']);

const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage },
  { id: 2235, color: 'blue', image: socksBlueImage },
]);

const cart = ref(0);

const addToCart = () => cart.value++;

const updateImage = (hoverImage) => (image.value = hoverImage);
</script>

<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart{{ cart }}</div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img :src="image" alt="socks" />
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>

        <div
          v-for="{ id, color, image } in variants"
          :key="id"
          @mouseover="() => updateImage(image)"
          class="color-circle"
          :style="{ backgroundColor: color }"
        ></div>
      </div>
      <button
        class="button"
        :class="{ disabledButton: !inStock }"
        @click="addToCart"
        :disabled="!inStock"
      >
        Add to Cart
      </button>
    </div>
  </div>
</template>
