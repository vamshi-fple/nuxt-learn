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
  
  <style scoped>
  .form-container {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 70vh;
    background: #f9fafb;
  }
  
  form {
    display: flex;
    flex-direction: column;
    background: white;
    padding: 2rem;
    border-radius: 10px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    width: 300px;
  }
  
  input {
    padding: 0.75rem 1rem;
    margin-bottom: 1rem;
    border: 1px solid #ddd;
    border-radius: 5px;
    font-size: 1rem;
    outline: none;
    transition: border-color 0.2s;
  }
  
  input:focus {
    border-color: #3b82f6;
  }
  
  button {
    padding: 0.75rem;
    background: #3b82f6;
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 1rem;
    cursor: pointer;
    transition: background 0.2s;
  }
  
  button:hover {
    background: #2563eb;
  }
  </style>
  