<template>
  <div v-if="!product" class="loading">Loading...</div>
  <div v-else>
    <div class="space-y-4">
      <div class="flex items-center bg-white rounded-lg shadow p-4">
        <img
          :src="product.image"
          alt=""
          class="w-24 h-24 object-contain rounded mr-4"
        />

        <div class="flex-1">
          <h4 class="text-lg font-semibold">{{ product.title }}</h4>
          <p class="text-gray-600">Category: ${{ product.category }}</p>
          <p class="text-gray-600">Price: ${{ product.price }}</p>
          <p class="text-gray-600">Description: {{ product.description }}</p>
        </div>
        <div>
          <button class="btn btn-primary" @click="decrement">-</button>
          <span style="margin: 0 10px">{{ quantity }}</span>
          <button class="btn btn-primary" @click="increment">+</button>
        </div>
      </div>
    </div>

    <div class="text-right mt-4">
      <h3 class="text-xl font-bold">
        Total Amount: ${{ (product.price * quantity).toFixed(2) }}
      </h3>
    <button @click="addToCart" class="btn btn-primary">Add to Cart</button>

    </div>
  </div>
</template>

<script setup>
const route = useRoute();

const product = ref(null);
const quantity = ref(1);

const fetchProduct = async () => {
  const res = await fetch(
    `https://fakestoreapi.com/products/${route.params.id}`
  );
  product.value = await res.json();
};

onMounted(() => {
  fetchProduct();
});

const increment = () => {
  quantity.value++;
};

const decrement = () => {
  if (quantity.value > 1) quantity.value--;
};

const addToCart = () => {
  const cart = JSON.parse(localStorage.getItem("cart") || "[]");
  const existingIndex = cart.findIndex((item) => item.id === product.value.id);

  if (existingIndex !== -1) {
    cart[existingIndex].quantity += quantity.value;
  } else {
    cart.push({ ...product.value, quantity: quantity.value });
  }

  localStorage.setItem("cart", JSON.stringify(cart));
  window.dispatchEvent(new Event("storage"));
  navigateTo("/cart");
};
</script>

