<template>
  <v-container>
    <h1 class="text-center mb-5">{{ title }}</h1>
    <v-row class="my-10">
      <h3>Calculator</h3>
      <v-btn 
        small 
        class="ml-3" 
        @click="showCalculator = !showCalculator"
        color="primary"
      >show</v-btn>
    </v-row>
    <Calculator :class="{showCalculator: showCalculator}" @changeTitle="updateTitle($event)"/>
    <v-row class="my-10">
      <h3>User List</h3>
      <v-btn 
        small 
        class="ml-3" 
        @click="showList = !showList"
        color="primary"
      >show</v-btn>
    </v-row>
    <v-data-table
      :class="{showList: showList}"
      :loading="loading"
      :headers="headers"
      :items="users"
      :items-per-page="6"
    >
      <template v-slot:[`item.detail`]="{ item }">
        <a @click="detail(item.id)">
          <v-btn icon><v-icon small>mdi-arrow-right-circle</v-icon></v-btn>
        </a>
      </template>
    </v-data-table>
    <addNewDialog 
      :class="{showList: showList}"
    />
  </v-container>
</template>

<script>
import Calculator from '../components/Calculator.vue';
import addNewDialog from '../components/addNewDialog.vue';

export default {
  name: 'Home',
  components: {
    Calculator,
    addNewDialog: addNewDialog
  },
  data: () => ({
    headers: [
      {text: "First Name", value: "first_name"}, 
      {text: "Last Name", value: "last_name"}, 
      {text: "Email Address", value: "email", sortable: false},
      {text: "Detail", value: "detail", sortable: false},
    ],
    users: [],
    loading: false,
    error: "",
    showCalculator: false,
    showList: false,
    title: "Welcome"
  }),
  methods: {
    initialize(){
      this.loading = true;
      fetch("https://reqres.in/api/users")
        .then(response => {
          if(response.status !== 200){
            this.error = "could not fetch data";
            this.loading = false;
          }
          return response.json();
        })
        .then( data => {
          this.users = data.data;
          this.loading = false;
        })
    },
    detail(id){
      this.$router.push({ name: "user", params: { id: id}});
    },
    updateTitle(newTitle){
      this.title = newTitle;
    }
  },
  created() {
    this.initialize();
  }
}
</script>

<style scoped>
.showCalculator{
  display: none;
}

.showList{
  display: none;
}
</style>