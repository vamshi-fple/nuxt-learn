<template>
  <div>Test</div>
</template>
<script setup>
definePageMeta({ layout: "default" });
onMounted(() => {
  navigateTo("/products");
});
</script>