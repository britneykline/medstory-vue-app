<template>
  <div class="vaccines-new">
    <form v-on:submit.prevent="submit()">
      <h1>Vaccine Create</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }} </li>
      </ul>
      <div>
        <label>Title:</label>
          <select v-model="newVaccineParams.title">
            <option disabled value="">Please select one</option>
            <option>Pfizer</option>
            <option>Moderna</option>
            <option>Johnson & Johnson</option>
          </select>
        </div>
        <div>
          <label>First Dose Date:</label>
          <input type="date" v-model="newVaccineParams.dose1_date" v-on:change="addSecondDoseDate" />
        </div>
        <div>
          <label>Second Dose Date:</label>
          <input type="date" v-model="newVaccineParams.dose2_date" />
        </div>
        <input type="submit" value="Submit" />
    </form>
    <button v-on:click="addSecondDoseDate">hello</button> 
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
    },
    addSecondDoseDate: function () {
      console.log("hello")
      Date.prototype.addDays = function(days) {
        var date = new Date(this.valueOf());
        date.setDate(date.getDate() + days);
        return date;
      }
      console.log(this.newVaccineParams.dose1_date);
      var date = new Date(this.newVaccineParams.dose1_date);

      console.log(date.addDays(22).toISOString().split('T')[0]);
      if (this.newVaccineParams.title == "Pfizer") {
        this.newVaccineParams.dose2_date = date.addDays(21).toISOString().split('T')[0];
      } 
      if (this.newVaccineParams.title == "Moderna") {
        this.newVaccineParams.dose2_date = date.addDays(28).toISOString().split('T')[0];
      } 
      if (this.newVaccineParams.title == "Johnson & Johnson") {
        this.newVaccineParams.dose2_date = date.addDays(0).toISOString().split('T')[0];
      } 
    }
  }
};
</script>