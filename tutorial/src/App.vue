<template>
  <div id="app">
    <div>{{fullName}} (@{{user.username}})</div>
    <span class="followers">Followers: {{followers}}</span>
    <button @click="followUser">Follow {{user.firstName}}</button>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return{
      followers: 0,
      user: {
        id: 1,
        username: 'emfl_api',
        url: 'https://twitter.com/emfl_api',
        firstName: 'Subrata',
        lastName: 'Sarkar',
        email: 'subrata@emfluence.com',
        isAdmin: false
      }
    }
  },
  computed: {
    fullName(){
      return `${this.user.firstName} ${this.user.lastName}`;
    },
    fullNameUS(){
      return `${this.user.lastName} ${this.user.firstName}`;
    }
  },

  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if( newFollowerCount > oldFollowerCount ) {
        //console.log('New follower added');
        //Do something real here...
      }
    }
  },

  methods: {
    followUser() {
      this.followers++;
    }
  },
  
  mounted() {
    this.followUser();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.followers {
    color:blueviolet;
    font-weight: bold;
}

button {
  width: auto;
}
</style>
