<template>
  <div style="display: contents"> <!-- my wrapper div is rendered invisible -->

  <article id="work" class="wrapper style2">
  <div class="container">
    <header>
      <h2>Your Vaccine</h2>
      <p>Vaccine information will populate here when you input a new vaccine.</p>
      <p></p>
    </header>
    <div class="row aln-center">
      <div class="col-4 col-6-medium col-12-small">
        <section class="box style1">
          <h3>Vaccine Specs</h3> 
            <p><b>Title:</b> {{ vaccine.title }}</p>
            <p><b>First Dose Date:</b> {{ vaccine.dose1_date }}</p>
            <p><b>Second Dose Date:</b> {{ vaccine.dose2_date }}</p></p>
        </section>
      </div>
      <div class="col-4 col-6-medium col-12-small">
        <section class="box style1">
          <h3>Vaccine Image</h3>
          <p><img :src="vaccine.vac_image" style="width:60%;height:60%;"/></p>
        </section>
      </div>
    </div>
  </div>
  </article>
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
      axios.get(`/vaccines/${this.$route.params.id}`).then(response => {
        this.vaccine = response.data;
      })
    },

  }
}
</script>