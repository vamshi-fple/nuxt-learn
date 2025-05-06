<template>
  <header class="navbar-container">
    <nav class="custom-nav">
      <div class="nav-left">
        <NuxtLink to="/" class="nav-link" exact-active-class="active">Home</NuxtLink>
        <!-- <NuxtLink to="/blog" class="nav-link" exact-active-class="active">Products</NuxtLink> -->
      </div>
      <div class="nav-right">
        <NuxtLink to="/login" class="nav-link" exact-active-class="active">Login</NuxtLink>
        <NuxtLink to="/signup" class="nav-link" exact-active-class="active">Sign Up</NuxtLink>
      </div>
    </nav>
  </header>
</template>

<style scoped>
.navbar-container {
  display: flex;
  justify-content: center;
  background: #ffffff;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  padding: 1rem;
  border-radius: 10px;
  margin: 1rem auto;
}

.custom-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.nav-left,
.nav-right {
  display: flex;
  gap: 1rem;
}

.nav-link {
  color: #333;
  padding: 0.5rem 1rem;
  border-radius: 5px;
  transition: background 0.2s, color 0.2s;
  text-decoration: none;
}

.nav-link.active,
.nav-link:hover {
  background: #3b82f6;
  color: white;
}
</style>
