<script setup>
import { ref,computed } from 'vue'
  import axios from "axios"
  

let id = 0

const title = ref('')
const year = ref('')
const type = ref('')
const response = ref('JSON')
const movie = ref('')

function addTodo() {
  axios.post(`https://www.omdbapi.com/?s=${title.value||''}&apikey=a9ad8207&y=${year.value||''}`).then(response=>{
    movie.value=response.data.Search
  })
}

  
</script>

<template>
  <form @submit.prevent="addTodo">
    <div  style='display:flex'><div>電影名稱</div>            <input v-model="title"></div>
    <div>年分<input v-model="year"></div>
    <div>type
      <select v-model="type">
      <option selected value='movie'>movie</option>
      <option value='series'>series</option>
      <option value='episode'>episode</option>
      </select></div>
    <div>Response
      <select v-model="response">
      <option selected value='JSON'>JSON</option>
      </select></div>
    <button>搜尋</button>
  </form>
  <div v-for="movie in movie">
    <div>{{movie.Title}}</div>
    <div>{{movie.Year}}</div>
    <div>{{movie.Type}}</div>
    <div>{{movie.imdbID}}</div>
    <img  :src="movie.Poster"/>
  </div>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>