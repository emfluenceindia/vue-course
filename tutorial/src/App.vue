<template>
  <div id="app">
    <UserProfile />
  </div>
</template>

<script>

import UserProfile from "./components/UserProfile";
export default {
  name: 'App',
  components: { UserProfile }
}
</script>

<style>
body {
  background-color: gainsboro;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  text-align: center;
  color: #2c3e50;
}

</style>
