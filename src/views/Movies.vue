<template>
  <div class="home">
    <Navbar />
    <div class="container-fluid">
      <div class="row">
        <div
          class="col-sm-12 col-md-4 col-lg-3 mb-4"
          v-for="movie in movielist"
          :key="movie.id"
        >
          <MovieCard :movie="movie" />
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "@/layouts/Navbar.vue";
import Footer from "@/layouts/Footer.vue";
import MovieCard from "@/components/MovieCard.vue";
import axios from "axios";

export default {
  name: "movies",
  mounted() {
    axios({
      method: "GET",
      url: "assets/samplejson/movielist.json",
    }).then(
      (response) => {
        this.movielist = response.data;
      },
      (error) => {
        // eslint-disable-next-line
        console.error(error);
      }
    );
  },
  data() {
    return {
      movielist: [],
      selectedMovie: "",
    };
  },
  components: {
    Navbar,
    MovieCard,
    Footer,
  },
};
</script>

<style scoped>
@import "../assets/styles/common.css";
</style>
