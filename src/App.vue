<template>
  <Navbar :logo="logo_src" :alt="app_name" />  <!-- Chamada da imagem -->
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
    },
    data() {
      return{ 
      logo_src: "/img/logo.png", // caminho da imagem 
      app_name: "Make Your Burger"
      }
    }
  }
</script>

<style> /* estilo global */
  * {
    font-family: Helvetica;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container {
    margin: 50px;
    min-height: 250px;
  }

  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }
</style>
