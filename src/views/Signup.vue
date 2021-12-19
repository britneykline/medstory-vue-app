<template>
  <div class="signup">
    <article id="contact" class="wrapper style4">
    <div class="container medium">
    <header>
      <h2>Signup</h2>
      <p>Create an account to keep track of your vaccine!</p>
    </header>
    <div class="row">
      <div class="col-12">
        <form v-on:submit.prevent="submit()">
           <ul>
            <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
           </ul>
          <div class="row">
            <div class="col-6 col-12-small">
              <input type="text" v-model="newUserParams.f_name" placeholder="First Name" />
            </div>
            <div class="col-6 col-12-small">
              <input type="text" v-model="newUserParams.l_name" placeholder="Last Name" />
            </div>
            <div class="col-12">
              <input type="text" v-model="newUserParams.email" placeholder="Email" />
            </div>
            <div class="col-12">
              <input type="password" v-model="newUserParams.password" placeholder="Password"></input>
            </div>
            <div class="col-12">
              <input type="password" v-model="newUserParams.password_confirmation" placeholder="Password Confirmation"></input>
              <small v-if="newUserParams.password !== newUserParams.password_confirmation">Passwords must match</small>
            </div>
            <div class="col-12">
              <ul class="actions">
                <li><input type="submit" value="Create Account" /></li>
                <li><input type="reset" value="Clear Form" class="alt" /></li>
              </ul>
            </div>
          </div>
        </form>
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
      newUserParams: {
        f_name: "",
        l_name: "",
        email: "",
        password: "",
        password_confirmation: ""
      },
      errors: []
    };
  },
  methods: {
    submit: function () {
      console.log(this.newUserParams)
      axios
        .post("/users", this.newUserParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/login");
          alert("You have successfully signed up");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>