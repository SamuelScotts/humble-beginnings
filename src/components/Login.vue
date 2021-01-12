<template>
   <div class="wrapper">
         <v-form @submit.prevent="login">
            <v-container>
            <h1>Login Component</h1>
               <v-row>
                  <v-col cols="12" md="4">
                     <v-text-field v-model="email" label="E-mail" required></v-text-field>
                  </v-col>
               </v-row>
               
               <v-row>
                  <v-col cols="12" md="4">
                     <v-text-field v-model="password" label="Password" required></v-text-field>
                  </v-col>
               </v-row>

               <v-row>
                  <v-col cols="12" md="4">
                     <v-btn @click="login()">Login</v-btn>
                  </v-col>
               </v-row>
            </v-container>
         </v-form>
   </div>
</template>

<script>
import firebase from 'firebase';
//import db from "../firestore";

export default {
   name: 'Login',
   data(){
      return{
         email: '',
         password: '',
         successMessage: '',
         errorMessage: ''
      }
   },
   methods: {
      login(){
         firebase.auth().signInWithEmailAndPassword(this.email, this.password)
            .then(user => {
               user;
               this.$router.replace('dashboard');
            })
            .catch(err => {
               this.errorMessage = err.message
            });
      }
   }
}
</script>