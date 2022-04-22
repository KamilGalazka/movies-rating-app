<template>
  <the-header></the-header>
  <the-form></the-form>
  <movies-list></movies-list>
</template>

<script>
import TheHeader from "./components/TheHeader.vue";
import TheForm from "./components/TheForm.vue";
import MoviesList from "./components/MoviesList.vue";

export default {
  components: {
    TheHeader,
    TheForm,
    MoviesList,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");

* {
  box-sizing: border-box;
  font-family: "Roboto", sans-serif;
}

body {
  margin: 0px;
}
</style>
