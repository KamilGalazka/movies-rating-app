<template>
  <div class="form-container">
    <form @submit.prevent="saveForm">
      <div>
        <label for="title">Title:</label>
        <input type="text" name="title" class="text" v-model="title" />
      </div>
      <div>
        <label for="director">Director:</label>
        <input type="text" name="director" class="text" v-model="director" />
      </div>
      <div>
        <label for="year">Year:</label>
        <input type="number" name="year" class="text" v-model="year" />
      </div>
      <div>
        <label for="rate">Rate (1 to 5):</label>
        <input type="radio" name="rate" value="1" v-model="rate" />
        <input type="radio" name="rate" value="2" v-model="rate" />
        <input type="radio" name="rate" value="3" v-model="rate" />
        <input type="radio" name="rate" value="4" v-model="rate" />
        <input type="radio" name="rate" value="5" v-model="rate" />
      </div>
      <p v-if="isInvalid">Something is missing!</p>
      <input type="submit" value="Submit" class="button-input" />
    </form>
  </div>
</template>

<script>
export default {
  name: "TheForm",
  data() {
    return {
      movies: [],
      title: "",
      director: "",
      year: null,
      rate: null,
      isInvalid: false,
    };
  },
  methods: {
    saveForm() {
      if (
        this.title === "" ||
        this.director === "" ||
        this.year === null ||
        this.rate === null
      ) {
        this.isInvalid = true;
      } else {
        this.isInvalid = false;
        fetch(
          "https://vue-films-db-default-rtdb.firebaseio.com/moviesList.json",
          {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify({
              title: this.title,
              director: this.director,
              year: this.year,
              rate: this.rate,
            }),
          }
        ).then((response) => {
          if (response.ok) {
            console.log("OK");
          } else {
            console.log("NOT OK");
          }
        });

        this.title = "";
        this.director = "";
        this.year = "";
        this.rate = "";
      }
    },
  },
};
</script>

<style scoped>
div.form-container {
  width: 70%;
  margin: 50px auto;
  box-shadow: 3px 3px 3px gray;
  background-color: #f28705;
  border-radius: 10px;
}

form {
  position: relative;
  padding: 20px 0 100px;
}

form div {
  margin: 20px auto;
  text-align: center;
}

form div label {
  position: absolute;
  left: 25%;
  font-size: 1.2rem;
}

form div input.text {
  width: 300px;
}

.button-input {
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  width: 100px;
  height: 40px;
  margin-top: 20px;
  font-size: 1.5rem;
  background-color: #f23030;
  border: none;
  border-radius: 5px;
}

.button-input:hover {
  opacity: 0.8;
  cursor: pointer;
}

p {
  font-size: 1.6rem;
  color: red;
  text-align: center;
}
</style>