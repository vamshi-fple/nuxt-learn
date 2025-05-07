<template>
  <div>
    <nav>Admin Sidebar</nav>
    <div class="content">
      <Nuxt />
    </div>
  </div>
</template>


<script setup>
definePageMeta({
  middleware: "default",
});
</script>