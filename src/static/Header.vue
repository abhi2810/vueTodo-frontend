<template>
  <header class="header">
    <nav class="navbar navbar-dark bg-dark">
      <a class="navbar-brand" href="#">
        <img src="logo.png" width="30" height="30" class="d-inline-block align-top" alt>
        Vue Todo
      </a>
      <div id="nav">
        <router-link class="router" to="/">Home</router-link>
        <router-link class="router" to="/about">About</router-link>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: "Header"
};
</script>

<style scoped>
.router{
  cursor: pointer;
  margin: 15px;
  color: #fff;
}
</style>
