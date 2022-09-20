<template>
  <div class="vue-footer">
    <h2 class="logo-title" v-on:click="goToMainPage()">Test Task</h2>
  </div>
</template>

<script>
export default {
  name: "footer",
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
