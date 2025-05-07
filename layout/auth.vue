

<template>
    <AppHeader />
    <NuxtLayout>
        
        <div class="flex-1 overflow-auto p-4">
        <slot />
      
        
      </div>
    </NuxtLayout>
    <AppFooter />
  </template>
  
  <script setup>
definePageMeta({
  middleware: "default",
});
</script>
  <style scoped>
  
  
  .home {
    flex: 1;
    min-height: 70vh;
  }
  </style>
  