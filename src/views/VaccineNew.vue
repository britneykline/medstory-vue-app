<template>
  <div class="vaccines-new">
    <h1>New Vaccine</h1>
    <button @click="openUploadModal">Vaccine Image</button>
    <form v-on:submit.prevent="submit()">
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
        <p><input type="submit" value="Submit" /></p>
    </form>
    <div>
      <img :src="newVaccineParams.vac_image" />
    </div>
    
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
        dose2_date: "",
        vac_image: ""
      },
      errors: []
    };
  },
  mounted() {

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
    },
      openUploadModal() {
        window.cloudinary.openUploadWidget(
        { cloud_name: 'dfagfffdu',
          upload_preset: 'jqahjptj'
        },
        (error, result) => {
          if (!error && result && result.event === "success") {
            console.log('Done uploading..: ', result.info.secure_url); 
            this.newVaccineParams.vac_image = result.info.secure_url;
          }
        }).open();
    }
  }
}
</script>

