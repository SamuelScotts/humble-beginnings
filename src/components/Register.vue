<template>
   <div class="wrapper">
         <v-form>
            <v-container>
            <h1>Register Component</h1>
               <v-row>
                  <v-col cols="12" md="4">
                     <v-text-field v-model="userData.firstname" label="First name" req ></v-text-field>
                  </v-col>

                  <v-col cols="12" md="4">
                     <v-text-field v-model="userData.lastname" label="Last name" required></v-text-field>
                  </v-col>
               </v-row>

               <v-row>
                  <v-col cols="12" md="4">
                     <v-text-field v-model="userData.username" label="Username" required></v-text-field>
                  </v-col>

                  <v-col cols="12" md="4">
                     <v-text-field v-model="userData.email" label="E-mail" required></v-text-field>
                  </v-col>
               </v-row>
               
               <v-row>
                  <v-col cols="12" md="4">
                     <v-text-field v-model="userData.password" label="Password" required></v-text-field>
                  </v-col>
                  <v-col cols="12" md="4">
                     <v-btn @click="registerUser()">Submit</v-btn>
                  </v-col>
               </v-row>
            </v-container>
         </v-form>
   </div>
</template>

<script>
import firebase from 'firebase'
import db from '../firestore'

export default {
   name: 'Register',
   data(){
      return{
         userData: {
            firstname: '',
            lastname: '',
            username: '',
            email: '',
            password: '',
         },
         successMessage: '',
         errorMessage: ''
      }
   },
   methods:{
   registerUser(){
      firebase.auth().createUserWithEmailAndPassword(this.userData.email, this.userData.password)
         .then(() => {
            firebase.auth().currentUser.updateProfile({
               displayName: this.userData.username
            }).then(() => {
               db.collection('users').add({
                  firstname: this.userData.firstname,
                  lastname: this.userData.lastname,
                  username: this.userData.username,
                  email: this.userData.email,
               }).then(() => {
                  this.$router.replace('home');
               }).catch(err => {
                  this.errorMessage = err.message;
               });
            }).catch(err => {
               this.errorMessage = err.message;
            });
         }).catch(err => {
            this.errorMessage = err.message
         });
      }
   }
}
</script>