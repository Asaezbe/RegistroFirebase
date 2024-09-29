 
<template>
   <img src="./assets/img/social.jpg">
 <br>
<h2 v-if="!isLoggedIn" >Asegurate de estar registrado para saber mas</h2>
<br>
  <div class="section1">
  
      <router-link to="/">Nosotros</router-link>
      <router-link v-if="!isLoggedIn" to="/login">Login</router-link>
      <router-link v-if="!isLoggedIn" to="/registro">Registro</router-link>
      <router-link v-if="isLoggedIn" to="/about">Home</router-link>
      <button v-if="isLoggedIn" @click="logout">Cerrar Sesión</button>

      <router-view></router-view>
  </div>

</template>
 
<script>
 
import {auth, signOut, onAuthStateChanged} from './auth.js'
 
 
  export default {
 
     data(){  
        return {
          isLoggedIn: false
        }
     },
     created(){
        onAuthStateChanged(auth,(user)=>{
 
          if(user){
            this.isLoggedIn = true
          }else{
            this.isLoggedIn = false
          }
 
          // this.isLoggedIn = user ? true : false
          // this.isLoggedIn = !!user
 
        })
     },
     methods:{
      async logout(){
        await signOut(auth)
        this.$router.push('/login')
      }
     }
  }
</script>
 
<style scoped>
</style>
 