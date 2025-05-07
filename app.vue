

<template>
  <NuxtLayout :name="layout">
    <NuxtPage />
  </NuxtLayout>
</template>

<style scoped>


.home {
  flex: 1;
  min-height: 70vh;
}
</style>
<script setup>
const layout = "default";
</script>