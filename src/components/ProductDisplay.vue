<script setup>
import { ref } from 'vue';
import socksGreenImage from '@/assets/socks_green.jpeg';
import socksBlueImage from '@/assets/socks_blue.jpeg';
import { computed } from '@vue/reactivity';

const { premium } = defineProps({
  premium: Boolean,
});

const emit = defineEmits(['add-to-cart']);

const product = ref('Socks');
const brand = ref('Vue Mastery');

const selectedVariant = ref(0);

const details = ref(['50% cotton', '30% wool', '20% polyester']);

const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage, quantity: 50 },
  { id: 2235, color: 'blue', image: socksBlueImage, quantity: 0 },
]);

const title = computed(() => `${brand.value} ${product.value}`);

const image = computed(() => variants.value[selectedVariant.value].image);

const inStock = computed(
  () => variants.value[selectedVariant.value].quantity > 0
);

const shipping = computed(() => (premium ? 'free' : 2.99));

const addToCart = () =>
  emit('add-to-cart', variants.value[selectedVariant.value].id);

const updateVariant = (index) => {
  selectedVariant.value = index;
};
</script>

<template>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">
        <img :src="image" alt="socks" />
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <p>Shipping: {{ shipping }}</p>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>

        <div
          v-for="({ id, color }, index) in variants"
          :key="id"
          @mouseover="() => updateVariant(index)"
          class="color-circle"
          :style="{ backgroundColor: color }"
        ></div>

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
  </div>
</template>
