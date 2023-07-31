<template>
  <div id="app">
    <button @click="getfilms">看电影</button>
    <ul>
      <li v-for="item in films":key="item.filmId">
        <img width="100p" :src="item.poster" >
        <p>{{item.name}}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import 'animate.css';

axios.interceptors.request.use(function (config){
  document.getElementsByClassName('cover')[0].style.display = "block"
  return config;
},function (error){
  return Promise.reject(error);
});

axios.interceptors.response.use(function (response){
  document.getElementsByClassName('cover')[0].style.display = "none"
  return response;
},function (error){
  return Promise.reject(error);
});

export default {
  name: 'App',
  data() {
    return {
      films:[]
    }
  },
  methods:{
    getfilms() {
      axios('https://m.maizuo.com/gateway?cityId=440300&pageNum=1&pageSize=10&type=1&k=7371609',{
        headers:{
          'X-Host':'mall.film-ticket.film.list'
        }
      })
      .then(res=>res.data)
      .then(res=>{
        this.films=res.data.films
      })
    }
  }
}
</script>


