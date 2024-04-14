<script setup>
import axios from 'axios';
import { onMounted , ref } from 'vue';
const todos = ref([])

onMounted(() => {
  axios.get("http://localhost:3000/todos")
    .then(resp => {
      console.table(resp.data);
      todos.value = resp.data;    
    })
  }
)

const deleteTask = (id) => {
  axios.delete('http://localhost:3000/todos/' + id)
  .then(() => {
    todos.value = todos.value.filter(todo => todo.id != id)
  })
}

const complete = (id) => {
  axios.patch('http://localhost:3000/todos/' + id, {"done" : "true"})
  .then (() => {
    let o = todos.value.find((elem) => elem.id == id)
    let index = todos.value.indexOf(o)
    todos.value[index].done = "true"
  })
}


  const editItem = (id)=>{
    axios.delete('http://localhost:3000/todos/' + id)
    .then(()=>{

    })
  }

  


</script>

<template>
  <div class="container">
    <div class="row">
      <div class="card" v-for="t in todos" :key="t.id">
        <div class="card-body">
          <p v-if="t.done != 'true'" class=" card-text h3 text-center">{{ t.task }}</p>
          
          <p v-if="t.done != 'false'" class="text-light card-text h3 text-center">{{ t.task }}</p>
          
          <p class="card-text h5 text-center">{{ t.deadline }}</p>
        </div>
        <div class="card-footer">
          <p @click="deleteTask(t.id)" class="torles ">Törlés</p>
          <p @click="complete(t.id)" v-if="t.done != 'true'" class="kesz ">Kész</p>
          
        </div>
      </div>
    </div>
  </div>  

</template>
<style scoped>

.torles{
  background-color: red;
  text-align: center;
  width: 90px;
  border-radius: 15px;
  display: block;
}
.frisit{
  background-color: yellow;
  text-align: center;
  width: 90px;
  border-radius: 15px;
  display: block;
}
.card{
  text-align: center ;
  border: solid black 1px;
  border-radius: 19px;
  background-color: rgb(135, 205, 237);
  width: 200px;
}
.container{
  
  width: 350px;
  display: block;
  text-align: center;
}
.card-body{
  border: 1px solid black;
  border-radius: 15px;
  background-color: rgb(86, 212, 212);
  display: block;
  width: 150px;
}
.kesz{
  background-color: rgb(67, 105, 10);
  text-align: center;
  width: 90px;
  border-radius: 15px;
}
.card-footer{
  text-align: center;
  display: block;
}
div{
  text-align: center;
  margin: 10px;
  
}


</style>

