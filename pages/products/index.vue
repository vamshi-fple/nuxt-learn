<template>
    <AppHeader />
  <div v-if="!data" class="product-list">
    Loading...
  </div>
  <div v-else>
    <div class="product-list">
      <div
        v-for="product in data"
        :key="product.id"
        class="product-card"
      >
        <img :src="product.image" alt="Product Image" class="product-img" />

        <h3 class="product-title"  @click="()=>handleRouter(product.id)" >{{ product.title }} </h3>

        <p class="product-price">${{ product.price }}</p>

        <div class="product-rating">
          ⭐ {{ product.rating.rate }} ({{ product.rating.count }} reviews)
        </div>

        <p class="product-desc">
          {{ product.description.slice(0, 80) }}...
        </p>

        <div class="product-actions">
          <button class="btn btn-primary" @click="()=>handleRouter(product.id)">View</button>
          <button class="btn btn-secondary" @click="()=>addToCart(product.id)">Add to Cart</button>
        </div>
      </div>
    </div>
  </div>
  <AppFooter />
</template>

<script setup>
  definePageMeta({ layout: 'default' })

const { data } = await useFetch('https://fakestoreapi.com/products')

const addToCart = (id) => {
  const cart = JSON.parse(localStorage.getItem('cart') || '[]')
  const existingIndex = cart.findIndex((item) => item.id === id)

  if (existingIndex !== -1) {
    cart[existingIndex].quantity += 1  
  } else {
    const product = data.value.find((p) => p.id === id)
    cart.push({ ...product, quantity: 1 })  
  }

  localStorage.setItem('cart', JSON.stringify(cart))
  window.dispatchEvent(new Event('storage'))
  navigateTo('/cart')
}


const handleRouter =(id)=>{
  
  navigateTo(`/products/${id}`)
}
</script>
