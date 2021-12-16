<template>
  <div class="vaccines-show">
    <p><b>id:</b> {{ vaccine.id }}</p> 
    <p><b>Title:</b> {{ vaccine.title }}</p>
    <p><b>First Dose Date:</b> {{ vaccine.dose1_date }}</p>
    <p><b>Second Dose Date:</b> {{ vaccine.dose2_date }}</p>
    <p><b>Vaccine Image:</b></p>
    <img :src="vaccine.vac_image"
          width="50%"
          height="50%"
          border="1px solid black"/> 
  </div>
</template>

<style></style>

<script>
import axios from 'axios';
export default {
  data: function () {
    return {
      vaccine: {
        
      },
    };
  },
  created: function () {
    this.getVaccine();

  },
  methods: {
    getVaccine: function() {
      console.log('getting vaccine...')
      // console.log(this.$route.params.id);
      axios.get(`/vaccines/${this.$route.params.id}`).then(response => {
      // axios.get("/vaccines").then(response => {
        console.log(response.data);
        this.vaccine = response.data;
      })
    },

  }
}
</script>