<template>
  <div id="nav">
    <router-link to="/">Accueil</router-link> |
    <router-link to="/search">Recherche catégorie</router-link>
  </div>
</template>

<script>
export default {
  name: "Menu"
}
</script>
<style>


#nav {
  padding: 30px;
  text-align: center;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>