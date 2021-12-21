<template>
  <div id="app">
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

</template>

<style></style>