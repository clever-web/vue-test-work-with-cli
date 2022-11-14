<template>
  <div class="details">
    <Navbar />
    <div class="container">
      <div v-if="movieDetails.id">
        <div class="row">
          <div class="col-md-5 align-left">
            <h2>{{ movieDetails.name }}</h2>
            <img :src="movieDetails.poster" class="desc-img" />
            <div class="d-flex mt-3">
              <div :class="`badge-item ${(movieDetails.rating < 4 && movieDetails.rating > 0 && 'badge-red') || (movieDetails.rating < 7 && movieDetails.rating > 4 && 'badge-purple') || (movieDetails.rating < 10 && movieDetails.rating > 7 && 'badge-success')}`">
                <img src="../assets/icons/score.png" class="badge-icon" />
                <span class="badge-text">{{ movieDetails.rating }}</span>
              </div>

              <div class="badge-item badge-blue">
                <img src="../assets/icons/score.png" class="badge-icon" />
                <span class="badge-text">{{ movieDetails.genre }}</span>
              </div>

              <div class="badge-item badge-purple">
                <img src="../assets/icons/score.png" class="badge-icon" />
                <span class="badge-text">{{ movieDetails.duration }}</span>
              </div>
            </div>
          </div>
          <div class="col-md-7 align-left">
            <h2>Description</h2>
            <p>
              {{ movieDetails.description }}
            </p>
            <div v-if="movieDetails.trivia">
              <h2>Trivia</h2>
              <ul>
                <li v-for="triv in movieDetails.trivia" :key="triv">
                  {{ triv }}
                </li>
              </ul>
            </div>
            <div v-if="movieDetails.actors">
              <h2>Actors</h2>
              <ul>
                <li v-for="actor in movieDetails.actors" :key="actor.imdb_id">
                  <a :href="`https://www.imdb.com/name/${actor.imdb_id}`" target="_blank">{{ actor.name }}</a>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
import Navbar from "@/layouts/Navbar.vue";
import Footer from "@/layouts/Footer.vue";
// @ is an alias to /src
import axios from "axios";

export default {
  name: "moviedetails",
  mounted() {
    const API_URL =
      this.$route.params.id == 16
        ? `assets/samplejson/movie${this.$route.params.id}.json`
        : "assets/samplejson/movielist.json";
    axios({
      method: "GET",
      url: API_URL,
    }).then((response) => {
      this.movieDetails =
        this.$route.params.id == 16
          ? response.data
          : response.data.find(
              (res) => res.id === Number(this.$route.params.id)
            );
    });
  },
  data() {
    return {
      movieDetails: {},
    };
  },
  components: {
    Navbar,
    Footer,
  },
  methods: {
    goToMainPage: function() {
      this.$router.push("/");
    },
  },
};
</script>

<style scoped>
@import "../assets/styles/common.css";
</style>
