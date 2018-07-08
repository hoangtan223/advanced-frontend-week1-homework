<template>
  <div>
    <h1>IMDB movies:</h1>
    <div class="nav">
      <button @click="sortLowest()">Lowest rated</button>
      <button @click="sortHighest()">Highest rated</button>
    </div>
    <ul>
      <li v-for="(movie,index) in movies" :key="index" v-if="index < 15" :class=" movie.vote_average > 8.2 ? 'blue-background' : ''">
        {{movie.title}} <span>{{movie.vote_average}}</span>
      </li>
    </ul>
  </div>
</template>

<script>
import '../assets/css/ress.css'
import '../assets/css/style.css'

export default {
  name: 'MovieListing',
  data () {
    return { movies: [] }
  },
  mounted: function () {
    let self = this
    fetch('https://api.themoviedb.org/3/discover/movie?api_key=d993bdf37f8ab7c574c990434a85a69f&sort_by=popularity.desc').then(function (response) {
      return response.json()
    }).then(function (result) {
      self.movies = result.results
    })
  },
  methods: {
    sortLowest () {
      this.movies = this.movies.sort((a, b) => a.vote_average - b.vote_average)
    },
    sortHighest () {
      this.movies = this.movies.sort((a, b) => b.vote_average - a.vote_average)
    }
  }
}
</script>
