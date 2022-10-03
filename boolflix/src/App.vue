<template>
  <div id="app">
    <div>
      <input type="text" v-model="query"/> <button @click="search">Cerca</button>
    </div>

    <div class="card" v-for="movie in Film" :key="movie.id">
      <p>Titolo: {{movie.title}}</p> 
      <p>Original: {{movie.original_title}}</p>  
      <p>Voto: {{movie.vote_average}}</p> 
      <p>lingua: 
        <img class="bandiera" :src="getFlag(movie.original_language)"
                              :alt="movie.original_language"
                              >
      </p> 
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
      Film: []
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
            this.Film = response.data.results;
        }
      })
      .catch(error => {
        console.log(error.message)
      })
    },
    getFlag(country){
      switch(country){
        case 'en':{
          country = 'gb';
          break;
        }
        case 'ja':{
          country = 'jp'
          break;
        }
      }

      return `https://flagicons.lipis.dev/flags/1x1/${country}.svg`
    },
    
  },
}
</script>






<style lang="scss">
  .card{
    border: 1px solid black;
    margin: 10px 0;
  }
</style> 
