<template>
  <div class="vaccines-show">
    <p><b>id:</b> {{ vaccine.id }}</p> 
    <p><b>Title:</b> {{ vaccine.title }}</p>
    <p><b>First Dose Date:</b> {{ vaccine.dose1_date }}</p>
    <p><b>Second Dose Date:</b> {{ vaccine.dose2_date }}</p>
    <!-- creator's id, currentUser's id -->
    <!-- current user Id {{ typeof $parent.getUserId() }} <br />  -->
    <!-- <div> {{ log(msg) }} </div> -->
    <!-- Person who made vaccine Id {{ typeof vaccine.user_id }} -->
    <div v-if="vaccine.user_id == $parent.getUserId()">
      <p><router-link v-bind:to="`/vaccines/${vaccine.id}/edit`">Edit Vaccine</router-link></p>
      <button v-on:click="destroyVaccine()">Remove Vaccine</button>
    </div>
    <div class="container">
      <!-- Logged in? {{ $parent.isLoggedIn() }} -->
      <!-- User Id {{ $parent.getUserId() }} -->
    </div>
  </div>
</template>

<style></style>

<script>
import axios from 'axios';
export default {
  data: function () {
    return {
      message: "Welcome to the show!",
      vaccine: {
        
      }
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
    destroyVaccine: function() {
      console.log('destroying vaccine...')
      axios.delete(`/vaccines/${this.$route.params.id}`).then(response => {
        console.log(response.data);
        this.$router.push('/vaccines')
      })
    }
    // log(msg){
    //   console.log(msg);
    // }
  }
}
</script>