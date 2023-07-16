<template>
  <div class="home">
    <Navbar/>
    <Baner />
    <Row
      title="Trending Now"
      :fetchUrl="fetchrequest.fetchTrending"
      :isLargeRow="true"
    />
    <Row title="Comedy Movies" :fetchUrl="fetchrequest.fetchComedyMovies" />
    <Row title="Action Movies" :fetchUrl="fetchrequest.fetchActionMovies" />


    <Row title="Top Rated" :fetchUrl="fetchrequest.fetchTopRated" /> 
    
    <Row title="Horror Movies" :fetchUrl="fetchrequest.fetchHorrorMovies" />
    <Row title="Romance Movies" :fetchUrl="fetchrequest.fetchRomanceMovies" />
    <Row
      title="Documentaries Movies"
      :fetchUrl="fetchrequest.fetchDocumentaries"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import Row from "@/components/Row.vue";
import requests from "@/Requests/requests.js";
import Baner from '@/components/Baner.vue'
import Navbar from '@/components/Navbar.vue'
export default {
  name: "HomeView",
  components: { Row,Baner,Navbar},
  setup() {
    const fetchrequest = requests;

    return { fetchrequest };
  },
};
</script>

<style>
.home {
  margin: 0;
}
</style>
