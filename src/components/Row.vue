<template>
  <div class="row">
  <h2>{{ title }}</h2>
  <div class="row_posters">
      <img
      v-for="m in movies" :key="m.id"
         :class="`${isLargeRow ? 'row_poster  row_posterLarge' : 'row_poster'}`"
        :src="`${base_url}${isLargeRow ? m.poster_path : m.backdrop_path}`"
        :alt="m.name"
        @click="handleClick(m)"
      />
  </div>

  <div class="youtubeTab"  v-show="isHidden" >
     <youtube-vue3  :videoid="`${trailerUrl}`"  :loop="`${opt.loop}`" :autoplay="`${opt.autoplay}`" :width ="`${opt.width}`" :height="`${opt.height}`"  />
  </div>
  </div>
</template>

<script>
import { ref, watchEffect } from "vue";
import axios from "@/Requests/axios";
import { YoutubeVue3 } from 'youtube-vue3'
import movieTrailer from 'movie-trailer'

export default {
  props: ["title", "fetchUrl", "isLargeRow"],
  components: {
    YoutubeVue3
  },
  setup(props) {
    let movies = ref([]);
    const base_url = "https://image.tmdb.org/t/p/original"
    let trailerUrl = ref("")
    let isHidden = ref(false)
    const opt =ref({
      width : "100%", 
      height : "390px",
      video_id : trailerUrl.value,
      loop: 0,
      autoplay: 1
  })
    watchEffect(() => {
      async function fetchData() {
        const request = await axios.get(props.fetchUrl);
        movies.value = request.data.results;
        return request;
      }
      fetchData();
    });

    const handleClick=  async (m) =>{
      if(trailerUrl.value){
        trailerUrl.value=''
      }else{
           await movieTrailer(m?.title || m?.name || m?.original_name || "")
          .then(url => {
            const urlParams = new URLSearchParams(new URL(url).search)
            trailerUrl.value = urlParams.get('v')

          }).catch(err => console.log(err))
      }
       isHidden.value = !isHidden.value
      }

  
      
  
    return { movies, base_url, opt,isHidden, trailerUrl, handleClick };
  },
};
</script>

<style>
.row {
  color: white;
  margin-left: 20px;
}

.row_posters {
  display: flex;
  overflow-y: hidden;
  overflow-x: scroll;
  padding: 20px;
}

.row_posters::-webkit-scrollbar {
  display: none;
}

.row_poster {
  object-fit: contain;
  width: 100%;
  max-height: 100px ;
  margin-right: 50px;
  transition: transform 450ms;
  cursor: pointer;
}

.row_poster:hover {
  transform: scale(1.1);
}

.row_posterLarge {
  max-height: 250px !important;
}

.row_posterLarge:hover {
  transform: scale(1.11);
}
.youtubeTab{
  padding: 40px;
  color:white
}
</style>
