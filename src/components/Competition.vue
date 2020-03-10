
<template>
  <div>
    <input type='text' v-on:keyup.13="test">
    <ul >
      <li v-for="user in users" :key="user.id">
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
        form: {
          id: '',
          name: ''
        },
        users: [],
        updateSubmit: false,
        loading:false
    }
  },
  mounted() {
    this.load()
  },
  methods: {
      focusarea(id){
        const reqData={
        'params':{
          'areas':id
        }
      }
        const reqHeaders = {
        'headers':{
          'X-Auth-Token': '5a45b64133774a5faac9aa4286366db0'
        }
      }
        axios.get('http://api.football-data.org/v2/competitions?areas='+id,reqHeaders).then(res => {
        console.log(res.data.competitions)

      }).catch ((err) => {
        console.log(err);
        
      })
        console.log(id)
    },
  }
}
</script>