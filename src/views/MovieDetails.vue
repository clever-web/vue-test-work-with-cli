<template>
  <div class="home">
    <div class="vue-logo-back">
      <h2 class="logo-title" v-on:click="goToMainPage()">Test Task</h2>
    </div>
    <div class="container">
      <div v-if="movieDetails.id">
        <div class="row">
          <div class="col-md-5 align-left">
            <h2>{{ movieDetails.name }}</h2>
            <img :src="movieDetails.poster" class="desc-img" />
            <div class="d-flex mt-3">
              <div class="badge-item badge-success">
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
                  {{ actor.name }}
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";

export default {
  name: "customerdetails",
  mounted() {
    const API_URL =
      this.$route.params.id == 16
        ? `assets/samplejson/movie${this.$route.params.id}.json`
        : "assets/samplejson/movielist.json";
    axios({
      method: "GET",
      url: API_URL,
    }).then(
      (response) => {
        this.movieDetails =
          this.$route.params.id == 16
            ? response.data
            : response.data.find(
                (res) => res.id === Number(this.$route.params.id)
              );
      },
      (error) => {
        console.error(error);
      }
    );
  },
  data() {
    return {
      movieDetails: {},
    };
  },
  methods: {
    goToMainPage: function () {
      this.$router.push("/");
    },
  },
};
</script>

<style scoped>
@import "../assets/styles/common.css";
</style>