<template>
  <v-form>
    <v-container>
      <v-text-field
        v-model="message4"
        label="Write your name here, please"
        outlined
        clearable
      ></v-text-field>
    </v-container>
  </v-form>
</template>

<script>
import axios from 'axios';

export default {
  name: "Home",

  data: () => ({
    name: '',
    age: null,
    gender: null,
    nationality: null
  }),

  methods: {
    async agify (){
       axios
      .get('https://api.agify.io/?name=Ivan')
      .then(response => (this.age = response))
      console.log(this.age)
    },
    async genderize (){
       axios
      .get('https://api.agify.io/?name=Ivan')
      .then(response => (this.gender = response))
      console.log(this.gender)
    },
    async nationalize (){
       axios
      .get('https://api.agify.io/?name=Ivan')
      .then(response => (this.nationality = response))
      console.log(this.nationality)
    }
  },

  created() {
    this.agify();
    this.genderize();
    this.nationalize();
  }

};
</script>