<template>
  <div class="card">
    <div class="card-content">
      <div class="image-container">
        <img :src="anime.images.jpg.large_image_url" :alt="anime.title + ' Poster'" />
      </div>
      <div class="text-container">
        <h3 class="anime-title">{{ anime.title }}</h3>
          <p class="anime-info"><strong>Duration:</strong> 
            <span>{{ anime.duration }}</span></p>
        <p class="anime-info"><strong>Rating: </strong>
            <span>{{ anime.rating }}</span></p>
        <p class="anime-synopsis"><strong>Description: </strong>
            <span>{{ anime.synopsis }}</span></p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['anime']
}
</script>

<style>
.card {
  width: 100%; 
  padding: 0px 8px;
  margin-bottom: 30px;
  display: flex;
  flex-direction: column;
}
.card-content:hover {
    background-color: rgb(255 236 194 / 66%);
}

.card-content {
  display: flex;
  flex: 1;
  justify-content: space-between;
  align-items: center;
}
/* .image-container {
  flex: 0 0 auto;
  width: 33%; 
  max-width: 33%; 
} */

.image-container img {
  width: 100%;
  height: 300px;
  object-fit: cover;
  border-radius: 16px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.15);
  transition: 0.4s;
}

.text-container {
  flex: 1;
  padding-left: 16px;
}

h3 {
  color: #180045c4;
  transition: 0.4s;
  font-size: 24px;
  margin-bottom: 20px;
}

.anime-title {
  font-size: 50px; 
}

.card:hover img {
  transform: scale(1.05);
}

.anime-info {
  margin-bottom: 10px;
  margin-top: 10px;
  color: #180045c4;
  font-size: 30px; 
}

p {
  color: #180045c4;
}

.anime-info span{
    margin-left: 10px;
}


@media screen and (min-width: 500px) and (max-width: 800px) {
  .card-content {
    display: flex;
    flex-direction: column; 
  }
  .image-container img {
    width: 100%;
    display: flex;
    justify-content: center;
  }
  .text-container{
   margin-top: 20px;
  }
}
</style>
