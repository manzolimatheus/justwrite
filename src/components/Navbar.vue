<template>
  <nav>
    <router-link to="/"><ion-icon name="home-outline"></ion-icon></router-link>
    <router-link to="/notes"><ion-icon name="document-text-outline"></ion-icon></router-link>
  </nav>
</template>

<script>
export default {
    name: 'Navbar'
}
</script>

<style scoped>

nav{
    background-color: cornflowerblue;
    padding: 1%;
    text-align: center;
}

nav a{
    color: white;
    text-decoration: none;
    padding-inline: 2%;
}

nav ion-icon{
    font-size: 18pt;
}

nav button{
    background: none;
    border: 0;
    color: white;
    padding-inline: 2%;
}

</style>