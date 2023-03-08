<template>
  <div>
    <Banner />
    <div class="main-container">
      <h1>HapMed Clinical Group</h1>
      <ConsultaForm />
    </div>
  </div>
</template>

<script>
import Banner from '../components/Banner.vue'
import ConsultaForm from '../components/ConsultaForm.vue'

export default {
  name: 'Home',
  components: {
    Banner,
    ConsultaForm
  }
}

</script>
