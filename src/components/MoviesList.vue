<template>
  <div>
    <button @click="showListFun">{{ showList ? "HIDE" : "SHOW" }} list</button>
    <p v-if="dataIsLoading">Loading...</p>
    <button v-if="showList && !dataIsLoading" @click="updateList">
      refresh
    </button>
    <p v-if="showList && movies.length === 0 && !dataIsLoading">
      No stored movies ratings. Please start adding something.
    </p>
    <ul v-else-if="showList && !dataIsLoading && movies.length !== 0">
      <movie-rate
        v-for="movie in movies"
        :key="movie.id"
        :title="movie.title"
        :director="movie.director"
        :year="movie.year"
        :rate="movie.rate"
      >
      </movie-rate>
    </ul>
  </div>
</template>

<script>
import MovieRate from "./MovieRate.vue";

export default {
  components: {
    MovieRate,
  },
  data() {
    return {
      movies: [],
      showList: false,
      dataIsLoading: false,
    };
  },
  methods: {
    updateList() {
      this.dataIsLoading = true;
      fetch("https://vue-films-db-default-rtdb.firebaseio.com/moviesList.json")
        .then((response) => {
          if (response.ok) {
            return response.json();
          }
        })
        .then((data) => {
          this.dataIsLoading = false;
          const movies = [];
          for (const id in data) {
            movies.push({
              id: id,
              title: data[id].title,
              director: data[id].director,
              year: data[id].year,
              rate: data[id].rate,
            });
          }
          this.movies = movies;
        });
    },
    showListFun() {
      if (!this.showList) {
        this.updateList();
        this.showList = !this.showList;
      } else {
        this.showList = !this.showList;
      }
    },
  },
};
</script>

<style scoped>
div {
  display: flex;
  flex-direction: column;
  width: 70%;
  margin: 50px auto;
  box-shadow: 3px 3px 3px gray;
  background-color: #f29f05;
  border-radius: 10px;
}

button {
  width: 150px;
  height: 40px;
  margin: 20px auto;
  font-size: 1.5rem;
  background-color: #f23030;
  border: none;
  border-radius: 5px;
  text-transform: uppercase;
}

button:hover {
  opacity: 0.8;
  cursor: pointer;
}

p {
  font-size: 1.7rem;
  text-align: center;
}
</style>