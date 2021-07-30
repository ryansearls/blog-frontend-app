<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Navbar</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarNaVDropdown"
        aria-controls="navbarNavDropdown"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarNavDropdown">
        <ul class="navbar-nav">
          <li class="nav-item active">
            <a class="nav-link" href="/posts">Posts</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/about">About</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/posts/new">Create</a>
          </li>
          <li class="nav-item dropdown">
            <a
              class="nav-link dropdown-toggle"
              href="#"
              id="navbarDropdownMenuLink"
              role="button"
              data-toggle="dropdown"
              aria-haspopup="true"
              aria-expanded="false"
            >
              Users
            </a>
            <div class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
              <li v-if="!isLoggedIn()">
                <a class="dropdown-item" href="/signup">Signup</a>
              </li>
              <li v-if="!isLoggedIn()">
                <a class="dropdown-item" href="/login">Login</a>
              </li>
              <li v-if="isLoggedIn()">
                <a class="dropdown-item" href="/logout">Logout</a>
              </li>
            </div>
          </li>
        </ul>
      </div>
    </nav>
    <div id="nav">
      <li>
        <router-link to="/">Home</router-link>
      </li>
      |
      <li>
        <router-link to="/about">About</router-link>
      </li>
      |
      <li v-if="!isLoggedIn()">
        <router-link to="/signup">Signup</router-link>
      </li>
      |
      <li v-if="!isLoggedIn()">
        <router-link to="/login">Login</router-link>
      </li>
      |
      <li v-if="isLoggedIn()">
        <router-link to="/logout">Logout</router-link>
      </li>
      |
      <li>
        <router-link to="/posts">Posts</router-link>
      </li>
      |
      <li>
        <router-link to="/posts/new">New</router-link>
      </li>
    </div>
    <router-view />
  </div>
</template>

<style>
body {
  font-family: Century Gothic, CenturyGothic, AppleGothic, sans-serif !important;
  text-align: center;
  background-image: url("./assets/repeated-square/repeated-square.png");
}
</style>

<script>
// import axios from "axios";

export default {
  methods: {
    isLoggedIn: function () {
      if (localStorage.getItem("jwt")) {
        return true;
      } else {
        return false;
      }
    },
    getUserId: function () {
      return localStorage.getItem("user_id");
    },
  },
};
</script>
