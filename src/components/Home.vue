<template>
  <div class="home">
    <div class="main">
      <div class="alert">
        <span class="closebtn" @click="closeNotification">&times;</span>
        <strong>You can only select five (5) Movies from the list.</strong>
      </div>
      <form class="search-box" v-on:submit.prevent="getMovies">
        <label for="Movie Title">Movie Title</label>
        <i class="fas fa-search"></i>
        <input
          type="text"
          placeholder="Search your favorite movies to nominate"
          v-model="movieSearch"
          @keyup="getMovies"
        />
      </form>
      <div class="movie-list">
        <div class="result-nominee">
          <div v-if="movieSearch" class="result">
            <p v-if="movieSearch" class="searchPreview">
              Result for"{{ movieSearch }}"
            </p>
            <hr class="header-underline" />
            <div
              v-for="(movie, index) in movielist"
              :key="index"
              class="results-list"
            >
              <h1 class="title">{{ movie.Title }}</h1>
              <p class="date">({{ movie.Year }})</p>
              <button @click="nominateBtn(movie.Title)">Nominate</button>
            </div>
          </div>

          <div class="nominee" :class="{ nomiateeee: !nominationList.length > 0 }">
            <p class="nomineeTitle">Nominations</p>
            <hr class="header-underline" />
            <div
              v-for="(movie, index) in nominationList"
              :key="index"
              class="nominations-list"
            >
              <h1 class="title">{{ movie.Title }}</h1>
              <p class="date">({{ movie.Year }})</p>
              <button @click="deleteFromList(index)">Remove</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      movieSearch: "",
      movielist: [],
      nominationList: [],
      nominationCompleted: false,
    };
  },
  methods: {
    getMovies: async function () {
      const key = "7fc691ba";
      console.log(this.movieSearch);
      fetch(`http://www.omdbapi.com/?apikey=${key}&s=${this.movieSearch}`)
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          this.movielist = data.Search;
        });
    },
    nominateBtn(e) {
      if (this.nominationList.length < 5) {
        this.movielist.forEach((movie) => {
          if (movie.Title === e) {
            this.nominationList.push(movie);
            this.nominationCompleted = false;
          }
        });
        this.movielist = this.movielist.filter((movie) => movie.Title !== e);
      } else {
        this.nominationCompleted = true;
        document.querySelector(".alert").style.display = "block";
      }
    },
    deleteFromList(index) {
      this.nominationList.splice(index, 1);
      if (this.nominationList.length !== 5) {
        document.querySelector(".alert").style.display = "none";
      }
    },
    closeNotification: function () {
      const alert = document.querySelector(".alert");
      alert.style.display = "none"
    },
  },
};
</script>

<style scoped>
.home {
  padding-left: 32px;
  padding-right: 32px;
}
.search-box {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
}
.search-box label {
  color: #ffffff;
}

.search-box input {
  margin-top: 10px;
  display: block;
  appearance: none;
  border: none;
  outline: none;
  background: none;
}
.search-box input[type="text"] {
  width: 100%;
  color: #000;
  background-color: #fff;
  font-size: 20px;
  padding-left: 40px;
  padding-right: 10px;
  border-radius: 8px;
  height: 50px;
  margin-bottom: 15px;
  transition: 0.4s;
  box-sizing: border-box;
}
.search-box input[type="text"]::placeholder {
  color: #000000;
  font-style: italic;
}
.search-box input[type="text"]:focus {
  box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
}
.fa-search {
  position: absolute;
  margin-top: 47px;
  margin-left: 10px;
  font-size: 1.3rem;
  color: #000;
}

.alert {
  padding: 20px;
  background-color: #4caf50;
  color: white;
  opacity: 1;
  /* transition: opacity 0.6s; */
  margin-bottom: 15px;
  display: none;
  animation: fadeIn ease 2s;
  -webkit-animation: fadeIn ease 2s;
  -moz-animation: fadeIn ease 2s;
  -o-animation: fadeIn ease 2s;
  -ms-animation: fadeIn ease 2s;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@-moz-keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@-webkit-keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@-o-keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@-ms-keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

.closebtn {
  margin-left: 15px;
  color: white;
  font-weight: bold;
  float: right;
  font-size: 22px;
  line-height: 20px;
  cursor: pointer;
  transition: 0.3s;
}

.closebtn:hover {
  color: black;
}
.header-underline {
  margin-top: 5px;
  margin-bottom: 5px;
  border: 1px solid rgb(243, 241, 241);
}
.movie-list {
  padding: 10px;
  margin-top: 15px;
  margin-bottom: 10px;
}
.result-nominee {
  position: relative;
}
@media (max-width: 820px) {
  .result-nominee .result,
  .result-nominee .nominee {
    position: relative;
    width: 100%;
    margin-bottom: 20px;
  }
  .date {
    margin-left: 15px;
    margin-right: 15px;
  }
  .alert {
    width: 100%;
  }
}
.result {
  border-radius: 5px;
  width: 49%;
  padding: 10px;
  background: #ffffff;
  box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
  position: absolute;
  left: 0;
  font-style: italic;
}

.nominee {
  border-radius: 5px;
  width: 49%;
  padding: 10px;
  background: #ffffff;
  box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
  position: absolute;
  right: 0;
  font-style: italic;
}
.nomiateeee {
  display: none !important;
}
.results-list,
.nominations-list {
  display: flex;
  align-items: center;
  gap: 15px;
}
.results-list,
.nominations-list {
  margin-top: 15px;
}
.results-list .title,
.nominations-list .title {
  font-size: 1rem;
}
.results-list button,
.nominations-list button {
  padding: 6px;
  border-radius: 4px;
  padding-left: 6px;
  padding-right: 6px;
  cursor: pointer;
  background-color: #35495e;
  color: #fff;
  border: none;
  transition: 0.4s;
  outline: none;
  font-style: italic;
}
.results-list button:hover,
.nominations-list button:hover {
  background-color: #66788b;
}
</style>
