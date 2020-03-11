
<template>
  <div>
      <h1>Competition: {{liganame}}</h1>
    <input type='text' v-on:keyup.13="focusarea(id)">
    <ul >
      <li v-for="data in datas" :key="data.id">
        {{data.name}}
        <router-link :to="'/teamdetails/'+data.id+'/'+data.name"><button>See Details</button></router-link>
        <router-link :to="'team/'+data.id+'/'+data.name"><button>See Players</button></router-link>

      </li>
    </ul>
  </div>
</template>

<script>
/* eslint-disable */ 
import axios from 'axios'
export default {
    props:{
        id:String,
        liganame:String
    },
  data(){
    return{
        datas: []
    }
  },
  mounted() {
  
    this.showteam()
  },
  methods: {
      showteam(id){
        const reqHeaders = {
        'headers':{
          'X-Auth-Token': '5a45b64133774a5faac9aa4286366db0'
        }
      }
        axios.get('http://api.football-data.org/v2/competitions/'+this.id+'/teams',reqHeaders).then(res => {
        console.log('aaaa',res.data)
        this.datas = res.data.teams

      }).catch ((err) => {
        console.log(err);
        
      })
        console.log(id)
    },
  }
}
</script>