<template>
    <div class="p-4">
      <h2 class="text-2xl font-bold mb-4">Your Cart</h2>
  
      <div v-if="cart.length === 0" class="felx items-center">
        <p>Your cart is empty.</p>
        <p @click="navigateTo('/')"> Back to Home 🏠</p>
      </div>
  
      <div v-else>
        <div class="space-y-4">
          <div
            v-for="item in cart"
            :key="item.id"
            class="flex items-center bg-white rounded-lg shadow p-4"
          >
            <img :src="item.image" alt="" class="w-24 h-24 object-contain rounded mr-4" />
  
            <div class="flex-1">
              <h4 class="text-lg font-semibold">{{ item.title }}</h4>
              <p class="text-gray-600">Price: ${{ item.price }}</p>
              <p class="text-gray-600">Quantity: {{ item.quantity }}</p>
              <p class="font-bold">
                Total: ${{ (item.price * item.quantity).toFixed(2) }}
              </p>
            </div>
  
            <button
              @click="removeItem(item.id)"
              class="bg-red-500 text-white px-3 py-1 rounded hover:bg-red-600"
            >
              Remove
            </button>
          </div>
        </div>
  
        <div class="text-right mt-4">
          <h3 class="text-xl font-bold">
            Total Amount: ${{ totalAmount.toFixed(2) }}
          </h3>
          <button
            @click="clearCart"
            class="bg-red-600 text-white px-4 py-2 rounded mt-2 hover:bg-red-700"
          >
            Clear Cart
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted, computed } from 'vue'
  
  const cart = ref([])
  
  const loadCart = () => {
    cart.value = JSON.parse(localStorage.getItem('cart') || '[]')
  }
  
  onMounted(() => {
    loadCart()
  })
  
  const totalAmount = computed(() =>
    cart.value.reduce((sum, item) => sum + item.price * item.quantity, 0)
  )
  
  const removeItem = (id) => {
    cart.value = cart.value.filter((item) => item.id !== id)
    localStorage.setItem('cart', JSON.stringify(cart.value))
  }
  
  const clearCart = () => {
    cart.value = []
    localStorage.removeItem('cart')
  }
  </script>
  