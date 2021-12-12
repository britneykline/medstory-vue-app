<template>
  <div class="vaccines-new">
    <form v-on:submit.prevent="submit()">
      <h1>Vaccine Create</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }} </li>
      </ul>
      <div>
        <label>Title:</label>
          <input type="text" v-model="newVaccineParams.title" />
        </div>
        <div>
          <label>First Dose Date:</label>
          <input type="date" v-model="newVaccineParams.dose1_date" />
        </div>
        <div>
          <label>Second Dose Date:</label>
          <input type="date" v-model="newVaccineParams.dose2_date" />
        </div>
        <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newVaccineParams: {
        title: "",
        dose1_date: "",
        dose2_date: ""
      },
      errors: []
    };
  },
  methods: {
    submit: function () {
      axios
        .post("/vaccines", this.newVaccineParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/vaccines");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>