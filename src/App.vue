<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" width="20%">
    <nav>
        <router-link to="/">Home</router-link>
        <router-link to="/about">About</router-link>
      </nav>
    <router-view/>

  </div>
</template>

<script>
import Expenses from './components/Expenses.vue'

export default {
  name: 'app',
  components: {
    Expenses
  }
}
</script>

<style>
@import "https://stackpath.bootstrapcdn.com/bootstrap/4.2.1/css/bootstrap.min.css"; 
@import "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.min.css"; 
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css"; 
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body{
    background-image: url(assets/body_mask.png);
    background-repeat: no-repeat;
    background-size: cover;
}

ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }
  
  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }

  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }

  .holder {
    box-shadow: 0px 0px 40px lightgray;
    background: #fff;
  }
  input {
    width: calc(100%);
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background-color: #323333;
    color: #687F7F;
  }

  select{
    width: calc(30%);
    border: 0;
    padding: 10px;
    font-size: 1em;
    background-color: #323333;
    color: #687F7F;
  }

  .price{
    width: calc(38%);
    border: 0;
    padding: 10px;
    font-size: 1em;
    background-color: #323333;
    color: #687F7F;
  }
  .fa-minus-circle{
      float: right;
      cursor: pointer;
  }

  nav {
  padding: 20px 20px 20px 0;
}

nav a {
  padding: 10px;
  text-decoration: none;
  background: #fff;
  border-radius: 3px;
  color: rgb(0, 110, 255);
  font-weight: bold;
  margin-right: 15px;
}
</style>
