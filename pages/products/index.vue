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

<style scoped>
.product-list {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
  justify-items: center;
  padding: 16px;
}

.product-card {
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  overflow: hidden;
  width: 100%;
  display: flex;
  flex-direction: column;
  transition: transform 0.3s, box-shadow 0.3s;
}

.product-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.2);
}

.product-img {
  width: 100%;
  height: 200px;
  object-fit: contain;
  background: #f8f8f8;
}

.product-title {
  font-size: 1rem;
  font-weight: bold;
  margin: 12px;
  /* height: 40px; */
  overflow: hidden;
}

.product-price {
  font-size: 1.2rem;
  color: #1976d2;
  margin: 0 12px;
}

.product-rating {
  font-size: 0.9rem;
  color: #888;
  margin: 4px 12px;
}

.product-desc {
  font-size: 0.85rem;
  color: #555;
  margin: 0 12px 12px 12px;
  flex-grow: 1;
}

.product-actions {
  display: flex;
  justify-content: space-between;
  padding: 12px;
  border-top: 1px solid #eee;
}

.btn {
  border: none;
  padding: 8px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 0.9rem;
}

.btn-primary {
  background: #1976d2;
  color: white;
}

.btn-secondary {
  background: #eee;
  color: #333;
}

</style>
