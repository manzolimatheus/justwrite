<template>
  <div id="application">
    <Header/>
    <Navbar/>
   <router-view />
  </div>
  
</template>

<script>
import Header from '@/components/Header.vue'
import Navbar from '@/components/Navbar.vue'

export default{
  components:{
    Header,
    Navbar
  }
}
</script>


<style>
*{
  margin: 0;
  padding: 0;
}

</style>
