<!--Template is the HTML portion -->
<template>
 <div id="app">
   <UserProfile/>
 </div> 
</template>

<!--Template is the JS portion 
Here we're importing the HellowWorld Component-->
<script>
import UserProfile from './components/UserProfile.vue'

export default {
  name: 'App',
  components: {UserProfile}

}
</script>

<!--Template is the CSS portion -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #F3F5FA;
}
</style>
