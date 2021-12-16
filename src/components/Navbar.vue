<template>
  <nav class="mb-10">
    <v-toolbar color="primary">
      <v-toolbar-title class="font-weight-black white--text">Fintax Recruitment Project</v-toolbar-title>
      <v-spacer/>
      <v-btn
        @click="home()"
        text
        dark
      > Home </v-btn>

    </v-toolbar>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
  data: () => ({
    
  }),
  methods: {
    home(){
      this.$router.push({ path: '/' });
    }
  }
}
</script>

<style>

</style>