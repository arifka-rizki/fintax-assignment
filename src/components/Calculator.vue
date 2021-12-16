<template>
  <div>
    <v-form>
      <v-row justify="center">
        <v-col cols="2">
          <v-text-field
            v-model="var1"
            label="First number"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="1" align-self="center" class="text-center">
          <h3>{{ operator }}</h3>
        </v-col>
        <v-col cols="2">
          <v-text-field
            v-model="var2"
            label="Second number"
            required
          ></v-text-field>
        </v-col>
      </v-row>

      <v-row justify="center">
        <v-col cols="1">
          <v-btn 
          @click="calculate(var1, var2, 'plus')" 
          small
          color="primary"
        ><v-icon>mdi-plus</v-icon></v-btn>

        </v-col>
        <v-col cols="1">
          <v-btn 
          @click="calculate(var1, var2, 'minus')" 
          small
          color="primary"
        ><v-icon>mdi-minus</v-icon></v-btn>
        </v-col>
      </v-row>
    </v-form>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data: () => ({
    var1: 0,
    var2: 0,
    total: 0,
    operator: "?"
  }),
  methods: {
    calculate(a, b, operator){
      let A = parseInt(a);
      let B = parseInt(b);
      if(operator === "plus"){
        this.operator = "+";
        this.total = A+B;
      } else if(operator === "minus"){
        this.operator = "-";
        this.total = A-B;
      }
      this.$emit('changeTitle', `The total is ${this.total}`);
    },
  }
}
</script>