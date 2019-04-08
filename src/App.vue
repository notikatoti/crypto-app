<template>
  <div class="page-container">
    <md-toolbar class="md-primary">
      <img src="./assets/logo.png" alt="CryptoApp" width="30">
      <h3 class="md-title">CryptoApp</h3>
    </md-toolbar>
    <md-content>
      <Main />
    </md-content>
  </div>
</template>

<style>
</style>

<script>
import Main from './components/Main.vue'

export default {
  name: 'app',
  components: {
    Main
  }
}
</script>
