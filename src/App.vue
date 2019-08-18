<template>
  <div id="app" class="is-marginless is-paddingless">
    <div id="title" class="container is-center">
      <h1 class="title is-1 has-padding-1 is-bold is-family-monospace">CloudAppi User Manager</h1>
      <img src="./assets/cloudappi.png" class="imageContainer">
    </div>
    <div class="container">
     <div style="background-color: rgba(178, 173, 173, 0.6) ">
       <p class="is-warning is-size-5 is-medium">Type a name or email address into the search bar and click SEARCH to find a user.</p>
     </div>
     <div id="searchBar" class ="container is-fluid">
       <form class="field is-grouped">
        <input class="input is-primary is-rounded is-medium is-left is-half" type="text" placeholder="Name or Email Address..." @input="onTextInput" v-bind:key="searchText" :keyup:enter="filterUsers"/>
        <button class="button is-medium is-info is-uppercase is-rounded is-right" v-on:click="filterUsers()">Search</button>
       </form>
     </div>
  </div>
  <display-results></display-results>
  </div>
</template>

<script>
import DisplayResults from './components/DisplayResults.vue';

export default {
  name: "app",
  components: {
    "display-results": DisplayResults
  },
  props: {
    "filteredUsers": Array,
    "searchText": ''
  },
  data() {
    return {
      user: {
        id: Number,
        name: String,
        email: String
      },
      users: [],
      termChange: ''
    }
  },
  methods: {
    fetchUsers() {
      const users = [];
      fetch("https://my-user-manager.herokuapp.com/users")
        .then(response => response.json())
        .then(data => users.push(...data))
        .then(console.log(users))
        .catch(error => console.log(error))
    },
      onTextInput(event){
        this.$emit('termChange', event.target.value);
        console.log(event.target.value);
      },
      filterUsers(termChange){
          const regex = new RegExp(termChange, 'gi');
          return [filteredUsers].push(
            users.name.match(regex) || users.email.match(regex) 
          )
        }
    },
  mounted: function(){
    this.fetchUsers()
  }
}
</script>

<style>
#app {
  background: url('./assets/abstract-3557689_1920.jpg') no-repeat center center fixed;
   -webkit-background-size: cover;
   -moz-background-size: cover;
   -o-background-size: cover;
   background-size: cover;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

div {
  padding: 2rem;
}

.imageContainer {
  margin-left: auto;
  margin-right: auto;
}

</style>
