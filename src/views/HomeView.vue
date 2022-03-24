<template>
  <v-form>
    <v-container>
      <v-text-field
        label="Write your name here, please"
        outlined
        clearable
        @change="getName($event)"
      ></v-text-field>
      
    </v-container>
  </v-form>
</template>

<script>
import axios from 'axios';

export default {
  name: "Home",

  data: () => ({
    age: {},
    gender: {},
    nationality: {}
  }),

  methods: {
    getName(name){
      this.agify(name);
      this.genderize(name);
      this.nationalize(name);
    },
    async agify (name){
       axios
      .get('https://api.agify.io/?name=' + name)
      .then((response) => response.json())
      .then(data => (this.age = data))
      console.log(this.age)
    },
    async genderize (name){
       axios
      .get('https://api.agify.io/?name=' + name)
      .then((response) => response.json())
      .then(data => (this.gender = data))
      console.log(this.gender)
    },
    async nationalize (name){
       axios
      .get('https://api.agify.io/?name=' + name)
      .then((response) => response.json())
      .then(data => (this.nationality = data))
      console.log(this.nationality)
    }
  },
};
</script>