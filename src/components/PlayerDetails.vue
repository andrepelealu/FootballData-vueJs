
<template>
  <div>
      <h1>{{playername}}</h1>
      
      {{datas.name}}
      {{datas.dateOfBirth}}
      {{datas.countryOfBirth}}
      {{datas.nationality}}
      {{datas.position}}
      {{datas.shirtNumber}}
     
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
        datas: []
        
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
        axios.get('http://api.football-data.org/v2/players/'+this.id,reqHeaders).then(res => {
        console.log('jumlah array',res.data)
        this.datas = res.data
       

      }).catch ((err) => {
        console.log(err);
        
      })
        console.log(id)
    },
  }
}
</script>