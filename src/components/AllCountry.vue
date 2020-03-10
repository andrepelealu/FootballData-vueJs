
<template>
  <div>
    <input type='text' v-on:keyup.13="test">
    <ul >
      <li v-for="user in datas" :key="user.id">
        {{user.id}}
        <button @click="focusarea(user.id)">Details</button>
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