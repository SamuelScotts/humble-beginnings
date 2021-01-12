<template>
  <div>
    <v-app-bar dense dark>
      <v-toolbar-title><router-link to="/" class="Logo">Home</router-link></v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn>
        <router-link to="/login">Login</router-link>
      </v-btn>

      <v-btn @click="logout()">
        Logout
      </v-btn>

      <v-btn>
        <router-link to="/register">Register</router-link>
      </v-btn>
    </v-app-bar>
  </div>
</template>

<script>
   import firebase from 'firebase'
   export default {
      name: "NavBar",
      methods: {
         logout(){
            firebase.auth().signOut().then(() => {
               this.$router.replace('login');
            });
         }
      }
   }
</script>