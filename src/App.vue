<script>
export default {
  data: function () {
    return {
      isLoggedIn: false,
    }
  },
  watch: {
    $route: function () {
      this.isLoggedIn = !!localStorage.jwt;
    }
  }
}
</script>

<template>
  <nav>
    <router-link to="/products">Products</router-link>
    <span v-if="isLoggedIn"> |
      <router-link to="/cart">Cart</router-link>
    </span>
    <span v-if="!isLoggedIn"> |
      <router-link to="/signup">Sign Up</router-link>
    </span>
    <span v-if="!isLoggedIn"> |
      <router-link to="/login">Log In</router-link>
    </span>
    <span v-if="isLoggedIn"> |
      <router-link to="/logout">Log Out</router-link>
    </span>

  </nav>
  <router-view />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
