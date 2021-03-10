<template>
  <div id="app">   
    <Validator />
    <User />
  </div>
</template>

<script>
import Validator from './components/Validator.vue'
import User  from './components/User.vue'

export default {
  name: 'App',
  components: {
    Validator,
    User
  }
}
</script>

<style>
a {
  text-decoration:none;
  transition:all 0.2s linear;
}
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    }
    html {
    color: #333;
    font-size: 62.5%;
    font-family: "Open Sans", sans-serif;
    }
</style>
