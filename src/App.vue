<template>
  <div id="app">
<!--    <nav class="navbar">-->
<!--      <router-link class="menu" to="/">Home</router-link> |-->
<!--      <router-link class="menu" to="/register">Register</router-link>-->
<!--    </nav>-->
    <router-view/>
  </div>
</template>
<script>
export default {
  mounted () {
    if (localStorage.getItem('loginToken') !== null) {
      this.$router.push('/dashboard')
    } else {
      this.$router.push('/')
    }
  }
}
</script>
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
.navbar{
  background: #9693be;
}
nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}

</style>
