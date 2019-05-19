<template>
  <div id="app">

    <b-navbar toggleable="lg" type="dark" variant="info">
    <b-navbar-brand href="#">Shoping Cart</b-navbar-brand>

   <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
       <b-nav-item active><router-link to="/">Home</router-link> |</b-nav-item>
      <b-nav-item> <router-link to="/about">About</router-link></b-nav-item>
      </b-navbar-nav>
    </b-collapse>  
  </b-navbar>
  
    <router-view/>
  </div>
 
</template>

<style scoped>
/* #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
a {
  color: #ffffff;
}
</style>
