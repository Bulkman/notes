<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view></router-view>
    
  </div>
</template>
<script>

export default {
  name: 'App',
  
}
</script>
<style lang="css">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
}

#nav {
  padding: 10px 30px;
  background-color: #42b983;
  /* width: 100%; */
  
  margin: 0px 0px 15px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #ebc700;
}
@import '../node_modules/bootstrap/dist/css/bootstrap.min.css';
</style>
