

<template>
  <AppHeader />
  <NuxtLayout class="layouts" >

      <NuxtPage />
  
  </NuxtLayout>
  <AppFooter />
</template>

<script setup>
definePageMeta({
  middleware: "default",
});
</script>

