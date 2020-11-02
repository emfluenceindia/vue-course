<template>
  <div id="app">
    <div id="top-navigation">
      <div id="navbar">
        <div class="navigation__logo">
          <a href="/">Learn Vue JS Core</a>
        </div>
        <div class="navigation__user">
          <a href="https://twitter.com/emfl_api">@emfl_api</a>
        </div>
      </div>
    </div>
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

<style lang="scss">
body {
  background-color: gainsboro;
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  text-align: center;
  color: #2c3e50;

  #top-navigation {
    background: palevioletred;
    padding: 10px;
    box-sizing: border-box;

    #navbar {
      width: 92%;
      margin: 0 auto;
      display: flex;
      justify-content: space-between;
      padding: 5px;
      box-sizing: border-box;

      a {
        color: white;
        text-decoration: none;
        font-size: 14px;
      }
    }
  }
}

</style>
