<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>
  <router-view />
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Raleway:wght@300;500;700&display=swap");
body {
  font-family: "Raleway", sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background: #121212;
  color: white;
}
#nav {
  text-align: center;
  padding-top: 1em;
  padding-bottom: 1em;
  background: #472b4e;
}
#nav a {
  color: white;
  text-decoration: none;
}
</style>
