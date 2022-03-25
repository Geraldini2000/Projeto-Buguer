<template>
<Navbar /> 
  <router-view/>
<Footer />
</template>

<script>
// imports components
import Navbar from './components/Navbar.vue' 
import Footer from './components/Footer.vue' 

  export default {
    components: {
      Navbar,
      Footer
    }
  }
</script>


