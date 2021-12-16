<template>
  <v-app id="app">
    <Navbar></Navbar>
    <router-view/>
  </v-app>
</template>

<script>
import Navbar from '@/components/Navbar.vue'

export default {
  name: 'Home',
  components: {
    'Navbar': Navbar
  },
  data: () => ({
    title: "Welcome",
  })
}
</script>

<style>
  /* @import url('https://fonts.googleapis.com/css? family=Oxygen:300,400,700&display=swap');

  $body-font-family: 'Oxygen';

  #app {
   font-family: $body-font-family, sans-serif !important;
  } */
</style>
