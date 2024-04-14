<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
//import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  
    
<div style="background-color: rgb(135, 205, 237);">
  <a style="margin: 20px;"><RouterLink  to="/">Adatok</RouterLink></a>
  <a style="margin: 20px;" ><RouterLink to="/about">Fö oldal</RouterLink></a>
</div>
<RouterView />
</template>

<style scoped>
div a {
  text-decoration: none;
  color: black;
  background-color: aqua;
  width: 60px;
  height: 30px;
  display: inline-block;
  text-align: center;
  border-radius: 20px;
  margin-top: 5px;
}
div{
  text-align: center;

border-radius: 20px;
margin: 10px;
}
</style>
