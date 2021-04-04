<template>
  <Navbar/>
  <router-view/>
</template>

<script>
import Navbar from '@/components/Navbar.vue'

export default {
  name:'App',
  components: {
    Navbar
  }
}
</script>


<style>
.bg-color{
  background: #3859bb;
}

.bg-wheat{
  background-color: wheat;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
