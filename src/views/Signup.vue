<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Signup</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>First Name:</label>
        <input type="text" v-model="newUserParams.f_name" /> 
      </div>
      <div>
        <label>Last Name:</label>
        <input type="text" v-model="newUserParams.l_name" /> 
      </div>
      <div>
        <label>Email:</label>
        <input type="email" v-model="newUserParams.email" />
      </div>
      <div>
        <label>Password:</label>
        <input type="password" v-model="newUserParams.password" />
      </div>
      <div>
        <label>Password confirmation:</label>
        <input type="password" v-model="newUserParams.password_confirmation" />
        <small v-if="newUserParams.password !== newUserParams.password_confirmation">Passwords must match</small>
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
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>