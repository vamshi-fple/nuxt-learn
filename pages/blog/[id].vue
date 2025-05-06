<template>
  <h1>Product Details</h1>

  <div v-if="!product" class="loading">
    Loading...
  </div>

  <div v-else class="product-card">
    <img :src="product.image" alt="Product Image" class="product-img" />

    <h2 class="product-title">{{ product.title }}</h2>

    <p class="product-price">$ {{ product.price }}</p>

    <div class="product-rating">
      ⭐ {{ product.rating.rate }} / 5 ({{ product.rating.count }} reviews)
    </div>

    <p class="product-description">
      {{ product.description }}
    </p>

    <div class="product-actions">
      <button class="btn btn-primary">Add to Cart</button>
    </div>
  </div>
</template>

<script setup>
import { useRoute } from 'vue-router'

// Get the route params (assuming route like /product/:id)
const route = useRoute()
const productId = route.params.id || 1  // fallback to id=1 if no param

const { data: product, pending, error } = await useFetch(`https://fakestoreapi.com/products/${productId}`)

console.log(product.value, "Fetched product data")
</script>

<style >
.product-card {
  max-width: 330px;
  margin: 0 auto;
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  text-align: center;
}

.product-img {
  max-width: 100%;
  height: auto;
}

.product-title {
  margin: 1rem 0 0.5rem;
}

.product-price {
  font-size: 1.2rem;
  color: green;
}

.product-rating {
  margin: 0.5rem 0;
}

.product-description {
  margin: 1rem 0;
}

.btn {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn-primary {
  background: #007bff;
  color: white;
}

.loading {
  text-align: center;
  font-size: 1.5rem;
}
</style>
