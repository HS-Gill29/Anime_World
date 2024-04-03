<template>
  <div class="app">
    <header>
    <h1>
      <span class="anime">Anime </span>
    <span class="world">World</span>
    </h1>
    
    <form class="search-box" @submit.prevent = "handleSearch">
      <font-awesome-icon icon="search" class="search-icon" />
      <input type="search"
       class="search-bar"
       placeholder="Search for an anime..."
       required
       v-model="search_query"
       />
  
       
    </form>
</header>
<main>
  <div class="cards">
    <AnimeCard v-for="anime in animeList" :key="anime.mal_id"
               :type = "TV" :anime="anime"
    />
    

  </div>
  <!-- -- add here for my front page -->
</main>
    
  </div>
  </template>

<script>
 import { ref } from "vue";
import AnimeCard from './components/AnimeCard'

export default {
   components: {
    AnimeCard,
   
  },
  setup (){
    const search_query = ref("");
    const animeList = ref([])

    const handleSearch =  async () => {
      const res = await fetch(`https://api.jikan.moe/v4/anime?q=${search_query.value}`)
      const data = await res.json();
      animeList.value = data.data.filter(anime => anime.episodes > 0 && anime.type === "TV");

      search_query.value = ""; 
    }
    
   return{
    search_query,
    animeList,
    handleSearch

   }

  }
  
}
</script>

<style>
.app {
  min-height: 100vh; 
  background-color: #e0cdb7;
 
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, sans-serif;
}

a {
  text-decoration: none;
}

header {
  
  padding-top: 50px;
  padding-bottom: 50px;
}

header h1 {
  font-size: 40px;
  font-weight: 200;
  text-align: center;
  text-transform: uppercase;
  color:  rgb(41 129 166 / 71%);
}
.anime{
  font-weight: lighter;
  font-style:normal;
}


header h1:hover {
  color: #b3b3b3;
}

.search-box {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  padding-left: 20px;
  padding-right: 30px;
}


.search-bar {
  border: none;
  outline: none;
  background-color: #F3F3F3;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.15);
  display: block;
  width: 100%;
  max-width: 600px;
  padding: 15px 45px 15px 15px;
  border-radius: 8px;
  color: #313131;
  font-size: 24px;
  transition: 0.4s;
  margin-left: 20px;
}



.search-bar::placeholder {
  color: #AAA;
}

.search-bar:focus,
.search-bar:valid {
  color: #FFF;
  background-color: #313131;
  box-shadow: 0px 0px 0px rgba(0, 0, 0, 0.15);
}

main{
  max-width: 1200px;
  margin: 0 auto;
  padding-left: 30px;  
  padding-right: 30px;
}
.cards{
  display: flex;
  flex-wrap: wrap;
}

</style>
