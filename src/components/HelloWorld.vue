<template>
  <div class="hello">
    <input type="text" v-model="animalName" id="animalname">
    <input type="text" v-model="imageUrl" id="imageurl">
    <button @click="postanimal">Post</button>
    <button @click="getanimals">Get</button>

    <div v-for="animal in animalArr"
    :key="animal.animalId">
      {{animal.animalId}}
      <h1>{{animal.animalName}}</h1>  
      <img :src="animal.imageUrl" alt="">  
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data() {
    return {
      animalName: null,
      imageUrl: null,
      animalArr: []
    }
  },
  methods: {
    postanimal() {
      axios.request({
        url: "http://127.0.0.1:5000/api/animals",
        method: "POST",
        data :{
          animalName: this.animalName,
          imageUrl: this.imageUrl
        }
      }).then((response)=>{
        console.log(response);
        this.getanimals();
      }).catch((error)=>{
        console.log(error);
      })
    },
    getanimals(){
      axios.request({
        url: "http://127.0.0.1:5000/api/animals",
        method: "GET"
      }).then((response)=>{
        console.log(response);
        this.animalArr = response.data;
      }).catch((error)=>{
        console.log(error);
      })
    },
    
  },
  mounted () {
      this.getanimals;
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
