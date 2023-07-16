<template>
    <header class="banner" 
    :style="`background-image:url(https://image.tmdb.org/t/p/original/${movie?.backdrop_path})`" 
    >
         <div class="banner_contents">
            <h1 class="banner_title">{{ movie?.title || movie?.name || movie?.original_name }}</h1>
            <div class="banner_buttuns">
                <button class="banner_buttun">Play</button>
                <button class="banner_buttun">My List</button>
            </div>

            <h1 class="banner_description">{{truncate(movie?.overview,150) }}</h1>
         </div>
         <div class="banner--fadeBottom">

         </div>
    </header>
</template>

<script>
import { ref, watchEffect } from "vue";
import axios from "@/Requests/axios";
import requests from "@/Requests/requests";

export default {
    setup() {
        let movie = ref();

        watchEffect(() => {
            async function fetchData() {
                const request = await axios.get(requests.fetchTrending);
                movie.value = request.data.results[
                    Math.floor(Math.random() * request.data.results.length- 1)
                ];
                return request;
            }
            fetchData();
        });
        function truncate(str, n) {
            return str?.length > n ? str.substr(0, n - 1) + "..." : str;
        }
        return { movie,truncate };
    },
}
</script>

<style>
header{
   background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}
.banner{
    color:white;
    object-fit: contain;
    height: 448px;
}
.banner_contents{
    margin-left: 30px;
    padding-top: 140px;
    height: 190px;
}
.banner_title{
    font-size: 3rem ;
    font-weight: 800;
    padding-bottom:0.3rem ;
}
.banner_description{
    width:45rem;
    line-height: 1.3;
    font-size: 0.8rem;
    max-width: 360px;
    height: 80px;
}
.banner_buttun {
  cursor: pointer;
  color: white;
  outline: none;
  border: none;
  font-weight: 700;
  border-radius: 0.2vw;
  padding-left: 2rem;
  padding-right: 2rem;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  margin-right: 1rem;
  background-color: rgb(51, 51, 51, 0.5);

}
.banner_buttun:hover {
  color: #000;
  background-color: #e6e6e6;
  transition: all 0.2s;
}
.banner--fadeBottom {
  height: 7.4rem;
  background-image: linear-gradient(180deg, transparent, rgba(37, 37, 37, 0.61), #111);
}
</style>