<template>
  <div class="login">
    <article id="login" class="wrapper style4">
    <div class="container medium">
    <header>
      <h2>Login</h2>
      <p>Login to view your vaccine information</p>
    </header>
    <div class="row">
      <div class="col-12">
        <form v-on:submit.prevent="submit()">
           <ul>
            <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
           </ul>
            <div class="col-12">
              <input type="text" v-model="newSessionParams.email" placeholder="Email"/>
            </div>
            <div class="col-12">
              <input type="password" v-model="newSessionParams.password" placeholder="Password"/>
            </div>
            <div class="col-12">
              <ul class="actions">
                <li><input type="submit" value="Login" /></li>
              </ul>
            </div>
        </form>
      </div>
    </div>
    </div>
    </article>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newSessionParams: {},
      errors: []
    };
  },
  methods: {
    submit: function () {
      axios
        .post("/sessions", this.newSessionParams)
        .then((response) => {
          axios.defaults.headers.common["Authorization"] =
            "Bearer " + response.data.jwt;
          localStorage.setItem("jwt", response.data.jwt);
          localStorage.setItem("user_id", response.data.user_id);
          this.$router.push("/vaccines");
          alert("You have successfully logged in");
        })
        .catch((error) => {
          console.log(error.response);
          this.errors = ["Invalid email or password."];
          this.email = "";
          this.password = "";
        });
    }
  }
};
</script>