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
import axios from "axios";

export default {
  name: "Home",

  data: () => ({
    age: {},
    gender: {},
    nationality: {},
  }),

  methods: {
    getName(name) {
      this.agify(name);
      this.genderize(name);
      this.nationalize(name);
    },

    async agify(name) {
      let tempAge = await fetch("https://api.agify.io/?name=" + name);
      this.age = await tempAge.json();
      console.log(this.age.age)
    },
    async genderize(name) {
      let tempGender = await fetch("https://api.agify.io/?name=" + name);
      this.gender = await tempGender.json();
      console.log(this.gender.gender)
    },
    async nationalize(name) {
      let tempNationality = await fetch("https://api.agify.io/?name=" + name);
      this.nationality = await tempNationality.json();
      console.log(this.nationality.nationality)
    },
  },
};
</script>