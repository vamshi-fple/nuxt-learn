<template>

    <div>
      <NuxtRouteAnnouncer />

       <div>
           <p>Count: {{ counter }}</p>
           <button class="button" @click="handleClick">Increment</button>
           <button  @click="handleDecrement" class="bg-violet-500 hover:bg-violet-600 focus:outline-2 focus:outline-offset-2 focus:outline-violet-500 active:bg-violet-700 ...">
decrement</button>  
       </div>
  
    </div>

</template>
<script setup lang="js">
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
const counter = ref(0); // executes in server and client environments

const handleClick = () => {
    counter.value++; // executes only in a client environment
};
const handleDecrement =()=>{
  counter.value--;
}
</script>