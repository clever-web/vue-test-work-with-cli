<template>
  <div class="card" v-on:click="goToDetailsPage(movie.id)">
    <div class="card-body">
      <img :src="movie.poster" class="card-img" />
      <p class="card-title warp" >{{ movie.name }}</p>
      <p class="card-text">{{ movie.description }}</p>
      <div class="d-flex">
        <div class="badge-item badge-success">
          <img src="../assets/icons/score.png" class="badge-icon" />
          <span class="badge-text">{{ movie.rating }}</span>
        </div>

        <div class="badge-item badge-blue">
          <img src="../assets/icons/genre.png" class="badge-icon" />
          <span class="badge-text">{{ movie.genre }}</span>
        </div>

        <div class="badge-item badge-purple">
          <img src="../assets/icons/duration.png" class="badge-icon" />
          <span class="badge-text">{{ movie.duration }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "movie-card",
  props: {
    movie: Object,
  },
  methods: {
    goToDetailsPage: function (id) {
      this.$router.push("/movie/" + id);
    },
  },
};
</script>

<style scoped>
@import "../assets/styles/common.css";
</style>
