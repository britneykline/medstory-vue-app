<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Covid Statistics</router-link> |
      <router-link to="/about">About</router-link> |
      <router-link to="/signup">Signup</router-link> |
      <router-link to="/login">Login</router-link> |
      <router-link to="/logout">Logout</router-link> |
      <router-link to="/vaccineNew">New Vaccine</router-link> |
      <router-link to="/vaccines">Your Vaccine</router-link>
    </div> -->
    <!-- Nav -->
  <nav id="nav">
    <ul class="container">
      <li><a href="/">Covid Statistics</a></li>
      <li><a href="/signup">Signup</a></li>
      <li><a href="/login">Login</a></li>
      <li><a href="/vaccineNew">New Vaccine</a></li>
      <li><a href="/vaccines">Your Vaccine</a></li>
      <li><a href="/logout">Logout</a></li>
    </ul>
  </nav>

  <router-view />


  <!-- Footer -->
  <footer>
    <ul id="copyright">
      <li>&copy; Untitled. All rights reserved.</li>
      <li>Design: <a href="http://html5up.net">HTML5 UP</a></li>
    </ul>
  </footer>
  </div>
</article>
    <!-- <div class="container">
      <!-- Logged in? {{ isLoggedIn() }} -->
      <!-- User Id {{ getUserId() }} -->
    <!-- </div> -->
  </div>
</template>

<style></style>