<style scoped>

.container{
  border: solid black 1px;
  border-radius: 19px;
  width: 400px;
  height: 400px;
 display: inline-block;
  text-align: center;
  position: relative;
  background-color: aqua;
}
.form-control.mt-3{
  background-color: black;
  color:  white;
  width: 220px;
  height: 30px;
  border-radius: 15px;
  display: block;
  text-align: center;
  margin: 10px;
  position: relative;
  left: 75px;
}

</style>


<template>
  
  <div class="container">
    <h3 class="h3 text-center mt-3">Alap adatok megadása</h3>
      <form class="w-75 mx-auto" @submit.prevent="saveTask()">
        <input class="form-control mt-3" type="text" v-model.trim="task" placeholder="Név">
        <input class="form-control mt-3" type="password" v-model.trim="password" placeholder="Password">
        <input class="form-control mt-3" type="date" v-model.trim="date">
        <input class="btn btn-outline-primary form-control mt-3" type="submit" style="background-color: green;" value="Mentés">
      </form>
      <p v-if="!kitoltve" class="mt-5 text-center h4 text-danger" style="color: red;">Minden mezőt töltsd ki!</p> 
      <p v-if="sikeres" class="text-center h4 text-success" style="color: green;">Mentés sikerült!</p>
  </div>
</template>
<script setup>
import {onMounted, ref} from 'vue'
import axios from 'axios'
const task = ref("")
const password=ref("")
const date = ref("")
const kitoltve = ref(true)
const tasks = ref([])
const lastId = ref()
const sikeres = ref(false)

onMounted( () =>{
    axios.get('http://localhost:3000/todos')
    .then(resp => tasks.value = resp.data)
})

const saveTask = () => {
    lastId.value = tasks.value[tasks.value.length-1].id * 1 + 1;
    if (task.value.length < 3 || date.value.length != 10 || password.value.length <3){
        //Hiányos kitöltés
        kitoltve.value = false;
    }
    else{
        //Hiánytalan kitöltés
        kitoltve.value = true;
        axios.post('http://localhost:3000/todos', {
            'id' : String(lastId.value), 
            "task" : task.value,
            "password":password.value, 
            "deadline" : date.value})
            .then(() => {
              task.value =password.value= date.value = "";
              sikeres.value = true
              setTimeout(siker, 2000);
            })
    }
  const siker = () =>{
    sikeres.value = false;
  }  

}
</script>
