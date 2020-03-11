<style >
  .center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
</style>
<template>
<div>
  
  <div v-if="!loading" class="container">
      <h3 class="text-center">Team Info</h3>
      <p>Team Name: <b>{{datas.name}}</b></p>
      <p>Adress: <b>{{datas.address}}</b></p>
      <p>Phone Number: <b>{{datas.phone}}</b></p>
      <p>Official Website: <b>{{datas.website}}</b></p>
      <p>Founded Year: <b>{{datas.founded}}</b></p>
      <p>Team Venue: <b>{{datas.venue}}</b></p><br>
      <h4 class="text-center">Squad List</h4>
      <div class="input-group mb-12">
        <input v-model="search" type="text" class="form-control" placeholder="Type to search ..." aria-label="Username"/>
        
      </div>
      <p>Search for: <b>{{search}}</b></p>
     <table class="table">
        <thead>
          <tr>
            <th>#</th>
            <th>Squad Name</th>
            <th>More Info</th>
          </tr>
      </thead>
        <tbody>
          <tr v-for="squad in filteredDatas" :key="squad.id">
            <th></th>
            <td>{{squad.name}}</td>
            <th>
              <router-link :to="'/player/'+squad.id+'/'+squad.name">  <b-button variant="primary">More Info</b-button></router-link>
            </th>
          </tr>
        </tbody>
      </table>
      </div>
      <div v-else class="container"> 
          <img class="center" src="https://media.tenor.com/images/d5015577b1133a47299b149b6fab1aaa/tenor.gif" alt="loading">
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
        squads:[],
        loading:false,
        search:''
        
    }
  },
  mounted() {
  
    this.showdetails()
  },
  methods: {
      showdetails(id){
        this.loading=true
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
        this.loading = false

      }).catch ((err) => {
        console.log(err);
        
      })
        console.log(id)
    }
  },
    computed:{
    filteredDatas:function(){
      return this.squads.filter((squad)=>{
        return squad.name.toLowerCase().match(this.search.toLowerCase())
      })
    }
  }
}
</script>