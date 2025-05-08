<template>
    <div class="form-container">
      <form @submit.prevent="onsubmit">
        <input v-model="email" type="text" placeholder="Email"  required   />
        <input v-model="password" type="password" placeholder="Password"  required />
        <button type="submit">Submit</button>
      </form>
    </div>
    
  </template>
  
  <script setup>

definePageMeta({ layout: 'auth' })

  const email = ref('')
  const password = ref('')
  
  const onsubmit = async () => {
    try {
    
      const data = await useFetch('https://fakestoreapi.com/auth/login' , { email: email.value, password: password.value } )
      // console.log('Sending:', { email: email.value, password: password.value })
      localStorage.setItem("user" ,JSON.stringify(data) )
      navigateTo("/products");
    } catch (error) {
      console.log(error)
    }
  }
  </script>
  