<script setup>
defineProps({ reviews: Array });
</script>
<template>
  <div class="review-container">
    <h3>Reviews</h3>
    <ul>
      <li v-for="(review, index) in reviews" :key="index">
        <span>{{ review.name }} gave this {{ review.rating }} starts</span>
        <br />
        <span>{{ review.content }}</span>
      </li>
    </ul>
  </div>
</template>
