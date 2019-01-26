<template>
  <div id="app">
    <router-view :key="$route.fullPath"/>
  </div>
</template>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>

<style lang="scss">
@import  "../node_modules/bulma/bulma.sass";

$primary: #ef7a00;
$secondary: #076bbb;

.has-text-secondary {
  color: $secondary !important;
}

.button.is-primary {
  background-color: $secondary !important;
}

.navbar.is-primary {
  background-color: $primary !important;
}

</style>