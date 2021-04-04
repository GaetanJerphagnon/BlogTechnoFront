<template>
    <div id="nav" class="p-0 m-0">   
        <ol class="breadcrumb d-flex justify-content-start bg-secondary m-0">
            <li class="p-0 m-0"><router-link class="px-2" to="/">Home</router-link></li>
            <li><router-link class="px-2" to="/workouts">Workouts</router-link></li>
            <li><router-link class="px-2" to="/about">About</router-link></li>
            <li><router-link class="px-2" to="/contact">Contact</router-link></li>
        </ol>
  </div>
</template>

<script>
export default {
  name: 'Navbar',
  props: {
    menus: Array
  }
}
</script>

<style scoped>
#nav ol {
    border-radius: 0;
}

#nav a{
    color: rgb(43, 39, 30) !important;
}

#nav a:hover{
    text-shadow: 0 0 1px black !important;
    text-decoration: none;
}

#nav a.router-link-exact-active {
    color: wheat !important;
}


</style>