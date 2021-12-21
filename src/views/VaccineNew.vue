<template>
  <div class="New Vaccine">
    <article id="new vaccine" class="wrapper style4">
    <div class="container medium">
    <header>
      <h2>Vaccine Information</h2>
      <p>Input vaccine information below. You have the option to include a photo of your vaccination card for your records as well!</p>
    </header>
    <div class="row">
      <div class="col-12">
        <p><button @click="openUploadModal">Vaccine Image</button></p>
        <form v-on:submit.prevent="submit()">
           <ul>
            <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
           </ul>
          <div class="row">
            <div class="col-12">
              <h2>Title:</h2>
                <select v-model="newVaccineParams.title">
                  <option disabled value="">Please select one</option>
                  <option>Pfizer</option>
                  <option>Moderna</option>
                  <option>Johnson & Johnson</option>
                </select><br>
            </div>
            <div class="col-12">
              <h2>First Dose Date:</h2>
                <input type="date" v-model="newVaccineParams.dose1_date" v-on:change="addSecondDoseDate" placeholder="Date"/>
            </div>
            <div class="col-12">
              <h2>Second Dose Date:</h2>
                <input type="date" v-model="newVaccineParams.dose2_date" />
            </div>
            <div class="col-12">
              <ul class="actions">
                <li><input type="submit" value="Save Vaccine" /></li>
                <li><input type="reset" value="Clear Form" class="alt" /></li>
              </ul>
            </div>
          </div>
        </form>
        <div>
          <img :src="newVaccineParams.vac_image" />
        </div>
      </div>
      </div>
      </div>
    </article>
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
          this.$router.push("/vaccines");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    addSecondDoseDate: function () {
      Date.prototype.addDays = function(days) {
        var date = new Date(this.valueOf());
        date.setDate(date.getDate() + days);
        return date;
      }
      var date = new Date(this.newVaccineParams.dose1_date);
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

