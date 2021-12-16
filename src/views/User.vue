<template>
  <v-container>
    <v-card class="mx-auto pb-5" max-width="250">
      <img :src="user.avatar" width="250">
      <v-card-title>{{user.first_name}} {{user.last_name}}</v-card-title>
      <v-card-text>{{user.email}}</v-card-text>
      <v-card-actions>
        <v-btn
          text
          color="red"
          @click="deleteUser(user.id)"
        >
          Delete
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: 'User',
  data: () => ({
    error: "",
    user: {},
    loading: false
  }),
  methods: {
    initialize(){
    const id = this.$route.params.id;
      fetch(`https://reqres.in/api/users/${id}`)
        .then(response => {
          if(response.status !== 200){
            this.error = "could not fetch data";
          } else {
            return response.json();
          }
        })
        .then(data => {
          this.user = data.data;
        })
    },
    deleteUser(id){
      fetch(`https://reqres.in/api/users/${id}`, {method: 'DELETE'})
        .then(response => {
          console.log(response);
          this.$router.push('/')
        })
    }
  },
  created(){
    this.initialize(this.id);
  }
}
</script>

<style>

</style>