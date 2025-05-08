<template>
    <div class="form-container">
        <form @submit.prevent="onsubmit">
          <div> Register </div>
        <input v-model="email" type="text" placeholder="Email"  required   />
        <input v-model="password" type="password" placeholder="Password"  required />
        <input v-model="cpassword" type="password" placeholder="Confirm Password"  required />

        <button type="submit">Submit</button>
      </form>
    </div>
    
  </template>
  
  <script setup>

definePageMeta({ layout: 'auth' })

  const email = ref('')
  const password = ref('')
  const cpassword = ref('')
  
  const onsubmit = async () => {
    try {
    
      console.log('Sending:', { email: email.value, password: password.value  , cpassword :cpassword.value })
    } catch (error) {
      console.log(error)
    }
  }
  </script>
  
  