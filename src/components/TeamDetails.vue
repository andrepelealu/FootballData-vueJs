
<template>
  <div>
      <h1>{{teamname}}</h1>
      
        {{datas.name}}
      {{datas.address}}
      {{datas.phone}}
      {{datas.website}}
      {{datas.founded}}
      {{datas.venue}}
      <div>
        <ul>
        <li v-for="squad in squads" :key="squad.id"> 
          {{squad.name}} 
          <router-link :to="'/player/'+squad.id+'/'+squad.name"><button>test</button></router-link>
        </li>

        </ul>
      </div>
  </div>
</template>

<script>
/* eslint-disable */ 
import axios from 'axios'
export default {
    props:{
        id:String,
        teamname:String
    },
  data(){
    return{
        datas: [],
        squads:[]
        
    }
  },
  mounted() {
  
    this.showdetails()
  },
  methods: {
      showdetails(id){
        const reqHeaders = {
        'headers':{
          'X-Auth-Token': '5a45b64133774a5faac9aa4286366db0'
        }
      }
        axios.get('http://api.football-data.org/v2/teams/'+this.id,reqHeaders).then(res => {
        console.log('jumlah array',res.data.squad.length)
        console.log('jumlah array',res.data.squad)

        this.datas = res.data
        this.squads = res.data.squad
        this.teamlength = res.data.squad.length

      }).catch ((err) => {
        console.log(err);
        
      })
        console.log(id)
    },
  }
}
</script>