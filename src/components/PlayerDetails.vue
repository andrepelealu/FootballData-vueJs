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
      <h3 class="text-center">Squad Details</h3>
      <p>Name: <b>{{datas.name}}</b></p>
      <p>Date of Birth: <b>{{datas.dateOfBirth}}</b></p>
      <p>Country of Birth: <b>{{datas.countryOfBirth}}</b></p>
      <p>Nationality: <b>{{datas.nationality}}</b></p>
      <p>Position: <b>{{datas.position}}</b></p>
      <p>Shirt Number: <b>{{datas.shirtNumber}}</b></p>
     
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
        playername:String
    },
  data(){
    return{
        datas: [],
        loading:false
        
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
        axios.get('https://api.football-data.org/v2/players/'+this.id,reqHeaders).then(res => {
        this.datas = res.data
        this.loading=false
       

      }).catch ((err) => {
        console.log(err);
        
      })
        console.log(id)
    },
  }
}
</script>