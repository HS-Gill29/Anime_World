<template>
  <div class="app">
    <header >
      <a href="/">
<h1>
        <span class="anime">Anime </span>
        <span class="world">World</span>
      </h1> </a>
      <form class="search-box" @submit.prevent="handleSearch">
        <input type="search"
               class="search-bar"
               placeholder="   Search for an anime..."
               required
               v-model="search_query" />
        <svg class="search-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
          <path d="M416 208c0 45.9-14.9 88.3-40 122.7L502.6 457.4c12.5 12.5 12.5 32.8 0 45.3s-32.8 12.5-45.3 0L330.7 376c-34.4 25.2-76.8 40-122.7 40C93.1 416 0 322.9 0 208S93.1 0 208 0S416 93.1 416 208zM208 352a144 144 0 1 0 0-288 144 144 0 1 0 0 288z"/>
        </svg>
      </form>
    </header>
    <main>
      <div class="cards">
        <AnimeCard v-for="anime in animeList" :key="anime.mal_id"
                   :type="TV" :anime="anime" />
      </div>
    </main>
  </div>
</template>


<script>
 import {  ref } from "vue";
import AnimeCard from "./components/AnimeCard.vue";

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
    handleSearch,
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
  color:  #06c;
  cursor: pointer;
}
.anime{
  font-weight: lighter;
  font-style:normal;
}


header h1:hover {
  color: #180045;
}

.search-box {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  padding-left: 20px;
  padding-right: 30px;
}
.search-icon {
  position: absolute;
  width: 10px;  
  height: 10px; 
  position: absolute;
  left: 31%;  
  width: 20px;
  height: 20px;
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

.search-icon:focus{
  color: whitesmoke;
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
