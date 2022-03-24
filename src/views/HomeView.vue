<template>
  <v-form>
    <v-container>
      <v-text-field
        label="Write your name here, please"
        outlined
        clearable
        @change="getName($event)"
      ></v-text-field>
      <v-data-table
        :headers="headers"
        :items="finalData"
        :items-per-page="5"
        class="elevation-1"
      ></v-data-table>
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
    starterMixedData: [],
    finalData: [],
    headers: [
      {
        text: "Name",
        align: "start",
        sortable: false,
        value: "name",
      },
      { text: "Country", value: "country" },
      { text: "Probability", value: "nationality probabiliy" },
      { text: "Age", value: "age" },
      { text: "Gender", value: "gender" },
      { text: "Probability", value: "gender probability" },
    ],
  }),

  methods: {
    async getName(name) {
      this.finalData = [];

      await this.agify(name);
      await this.genderize(name);
      await this.nationalize(name);

      let firstArray = [];
      this.starterMixedData = [this.age, this.gender, this.nationality];
      this.starterMixedData = this.starterMixedData[2].country.forEach(
        (country) =>
          firstArray.push([
            this.starterMixedData[0],
            this.starterMixedData[1],
            country,
          ])
      );
      let secondArray = [];
      firstArray.forEach((array) =>
        secondArray.push({
          name: array[0].name,
          age: array[0].age,
          gender: array[1].gender,
          "gender probability": array[1].probability,
          country: array[2].country_id,
          "nationality probability": array[2].probability,
        })
      );
      secondArray.forEach((object) => this.finalData.push(object));
    },

    async agify(name) {
      let tempAge = await fetch("https://api.agify.io/?name=" + name);
      this.age = await tempAge.json();
      console.log(this.age.age);
    },
    async genderize(name) {
      let tempGender = await fetch("https://api.genderize.io/?name=" + name);
      this.gender = await tempGender.json();
      console.log(this.gender.gender);
    },
    async nationalize(name) {
      let tempNationality = await fetch(
        "https://api.nationalize.io/?name=" + name
      );
      this.nationality = await tempNationality.json();
      console.log(this.nationality.country);
    },
  },
};
</script>