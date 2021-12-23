<template>
  <div class="main-nav">
    <router-link :to="{ name: 'Home' }"> Projects </router-link>
    <router-link :to="{ name: 'AddProject' }"> Add a new project </router-link>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.main-nav {
  text-align: center;
  margin: 40px auto;
}

.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: #30475e;

  font-size: 18px;
}

a.router-link-active {
  border-bottom: 2px solid #3fa796;
}
</style>
