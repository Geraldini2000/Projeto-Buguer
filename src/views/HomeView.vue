<template>
  <Banner />
  <div class="main-container">
  <h1>Monte o seu burger:</h1>
  <BurgerForm />
  </div>
</template>

<script>
import Banner from '../components/Banner.vue' // Caminho componente de Banner
import BurgerForm from '../components/BurgerForm.vue' // Caminho componente de Formulario

  export default {
    name: 'Home',
    components: {
      Banner,
      BurgerForm,
    }
  }
</script>
