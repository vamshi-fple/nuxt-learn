<template>
  <header class="navbar-container">
    <nav class="custom-nav">
    <div class="nav-left">
      <NuxtLink to="/" class="nav-link" exact-active-class="active">Home</NuxtLink>
      <NuxtLink to="/products" class="nav-link" exact-active-class="active">Products</NuxtLink>
      <NuxtLink to="/products-list" class="nav-link" exact-active-class="active">List </NuxtLink>

    </div>
    <div class="nav-right">
      <NuxtLink to="/auth/login" class="nav-link" exact-active-class="active" v-if="!isLoggedIn">Login</NuxtLink>
      <NuxtLink to="/auth/signup" class="nav-link" exact-active-class="active" v-if="!isLoggedIn">Sign Up</NuxtLink>
      <NuxtLink to="/admin" class="nav-link" exact-active-class="active">Admin</NuxtLink>

      <!-- Show if logged in -->
      <NuxtLink to="/cart" class="nav-link" exact-active-class="active" v-if="isLoggedIn">🛒 Cart</NuxtLink>

      <!-- Profile with dropdown -->
      <div class="profile-wrapper" v-if="isLoggedIn" @click="toggleDropdown">
        <span class="nav-link">👤 Profile</span>
        <div class="dropdown" v-if="showDropdown">
          <NuxtLink to="/profile" class="dropdown-item">My Profile</NuxtLink>
          <button class="dropdown-item" @click.stop="logout">Logout</button>
        </div>
      </div>
    </div>
  </nav>
  </header>
</template>

<script>
  definePageMeta({ layout: 'default' })
  export default {
  data() {
    return {
      isLoggedIn: false,
      showDropdown: false
    };
  },
  mounted() {
    const user = localStorage.getItem('user');
    if (user) {
      this.isLoggedIn = true;
    }
  },
  methods: {
    toggleDropdown() {
      this.showDropdown = !this.showDropdown;
    },
    logout() {
      localStorage.removeItem('user');
      this.isLoggedIn = false;
      this.showDropdown = false;
      this.$router.push('/'); // Redirect to home or login page
    }
  }
}
</script>

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
  /* padding: 0.5rem 1rem; */
  border-radius: 5px;
  transition: background 0.2s, color 0.2s;
  text-decoration: none;
}

.nav-link.active,
.nav-link:hover {
  background: #3b82f6;
  color: white;
}
profile-wrapper {
  position: relative;
  display: inline-block;
  cursor: pointer;
}
.dropdown {
  position: absolute;
  right: 0;
  background: white;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  z-index: 10;
}
.dropdown-item {
  display: block;
  padding: 8px 12px;
  width: 150px;
  text-align: left;
  background: white;
  border: none;
  cursor: pointer;
}
.dropdown-item:hover {
  background: #f0f0f0;
}
</style>
