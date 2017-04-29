<template>
  <div id="app">
		<h1 class="title is-1">Movie Poster</h1>
		<form class="movie-form" @submit.prevent>
			<input type="text" class="input is-primary is-large" placeholder="Enter movie title here" v-model="movietitle" autofocus>
			<input type="submit" class="button is-primary is-large" @click="request" value="Get Movie Poster">
		</form>
		<div class="movie-poster"><img :src='movieposterurl'></div>
  </div>
</template>

<script>
var axios = require('axios');

const api_key = '4120175e535d978bf6f3785ea754ffc2';
export default {
  name: 'app',
  data() {
		return {
			movietitle: '',
			movieposterurl: 'https://image.tmdb.org/t/p/w342/kBf3g9crrADGMc2AMAMlLBgSm2h.jpg'
		}
  },
	methods: {
		request () {
			axios.get('https://api.themoviedb.org/3/search/movie?query=' + this.movietitle + '&api_key=' + api_key).then((response) => {
				this.movieposterurl = 'https://image.tmdb.org/t/p/original' + response.data.results[0].poster_path;
			});
		}
	}
}
</script>

<style lang="scss">
@import '~bulma/bulma.sass';

#app {
	margin-top: 1em;
	text-align: center;
}
div, form {
	margin: 0 auto;
}
img {
	width: 100%;
	max-width: 342px;
}
input {
	margin-bottom: 0.5em;
}
.movie-form {
	max-width: 300px;
}
input[type=text] {
	text-align: center;
}
</style>
