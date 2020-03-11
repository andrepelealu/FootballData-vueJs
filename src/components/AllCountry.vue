<style >
  .center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
</style>
<template>
<div class="container">
    <div v-if="!loading" >
      <h3 class="text-center">Show all country</h3>
      <div class="input-group mb-3">
        <input v-model="search" type="text" class="form-control" placeholder="Type to search ..." aria-label="Username"/>
        
      </div>
      <p>Search for: <b>{{search}}</b></p>
      <table class="table">
        <thead>
          <tr>
            <th>#</th>
            <th>Country</th>
            <th>Details</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="data in filteredDatas" :key="data.id">
            <th></th>
            <td>{{data.name}}</td>
            <th>
              <router-link :to="'/country/'+data.id+'/'+data.name">  <b-button variant="primary">Details</b-button></router-link>
            </th>
          </tr>
        </tbody>
      </table>
    </div>
    <div v-else>
      <img class="center" src="https://media.tenor.com/images/d5015577b1133a47299b149b6fab1aaa/tenor.gif" alt="loading">
    </div>
  </div>
</template>



<script>
/* eslint-disable */ 
import axios from 'axios'
export default {
  data(){
    return{
        datas: [],
        loading:false,
        search:''
    }
  },
  mounted() {
    this.load()
  },
  methods: {
    load(){
      this.loading=true
      const reqHeaders = {
        'headers':{
          'X-Auth-Token': '5a45b64133774a5faac9aa4286366db0'
        }
      }
        axios.get('https://api.football-data.org/v2/areas',reqHeaders).then(res => {
        this.datas = res.data.areas
        this.loading=false
        console(this.search)
      }).catch ((err) => {
        console.log(err);
        
      })
    }
  },
  computed:{
    filteredDatas:function(){
      return this.datas.filter((data)=>{
        return data.name.toLowerCase().match(this.search.toLowerCase())
      })
    }
  }
}
</script>