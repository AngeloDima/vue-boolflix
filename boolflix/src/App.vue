<template>
  <div id="app">
    <div>
      <input type="text" v-model="query"/> <button @click="search">Cerca</button>
    </div>
  </div>
</template>

<script>
  import axios from "axios";

export default {
  name: 'App',
  data(){
    return {
      query: ``,
      movies: []
    }
  },
  methods:{
    search(){
      this.queryApi(this.query);
    },
    queryApi(textToSearch){
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=c4843b621764220065cb747f4ce24763&query=${textToSearch}&language=it-IT`)
        .then((response)=>{
          console.log(response);
          if (response.status === 200){
            this.movies = response.data.results;
        }
      })
      .catch(error => {
        console.log(error.message)
      })
    }
  },
}
</script>






<style lang="scss">

</style> 
