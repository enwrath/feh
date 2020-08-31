<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Legendary/Mythic Calendar</router-link> |
      <router-link to="/arenascore">Arena Score</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

#nav {
  padding: 30px;
  background-color: #150101;
}

a {
  color: #86b2de;
}

a.router-link-exact-active {
  color: #a4e6c8;
}
body {
  color: #e6e2e2;
  background-color: #242a53;
}
</style>
