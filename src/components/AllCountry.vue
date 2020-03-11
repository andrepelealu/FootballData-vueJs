
<template>
  <div>
    <h1>Show all country</h1>
    <input type='text' v-on:keyup.13="test">
    <ul >
      <li v-for="data in datas" :key="data.id">
        {{data.name}}
        <router-link :to="'/country/'+data.id+'/'+data.name"><button>Details</button></router-link>
      </li>
    </ul>
  </div>
</template>

<script>
/* eslint-disable */ 
import axios from 'axios'
export default {
  data(){
    return{
        datas: [],
        loading:false
    }
  },
  mounted() {
    this.load()
  },
  methods: {
    load(){
      const reqHeaders = {
        'headers':{
          'X-Auth-Token': '5a45b64133774a5faac9aa4286366db0'
        }
      }
        axios.get('http://api.football-data.org/v2/areas',reqHeaders).then(res => {
        this.datas = res.data.areas
      }).catch ((err) => {
        console.log(err);
        
      })
    },
    test(){
        alert('coba')
      }
  }
}
</script>