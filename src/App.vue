<template>
  <v-app id="app">
    <div id="nav">
       <v-btn
        to="/Signin"
       >
        Login
      </v-btn> 
       <v-btn
        to="/Signup"
       >
        Signup
      </v-btn> 
    </div>
    <router-view/>
  </v-app>
</template>

<script>
export default {

  data() {
    return {
    }
  }
}
</script> 
<style lang="scss">
@import "../node_modules/@aasaam/noto-font/dist/font-face.css" ;

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  font-family: 'aasaam-Noto';
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
