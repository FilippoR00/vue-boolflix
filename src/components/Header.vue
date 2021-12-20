<template>
	<div>
		<img src="..\assets\logo.png" alt="Logo">
		<input type="text" v-model="search" v-on:keyup.enter="getMovies">
		<button @click='getMovies'>Cerca</button>
	</div>
</template>

<script>
import axios from 'axios';
import dataShared from "../share/dataShared";

export default {
	name: 'Header',
	data() {
		return {
			search : '',
			dataShared,

		}
	},
	methods: {
		getMovies() {
			axios.get('https://api.themoviedb.org/3/search/movie', {
				params: {
					api_key : '0b9ac5d0a41cb0ca49e6d38df58bc461',
					language : 'it-IT',
					query : this.search
				}
			})
			.then(function (response) {
				dataShared.myData = response.data.results;
			})
			.catch(function (error) {
				console.log(error);
			});  
		}
	},
}
</script>

<style scoped lang="scss">
	
</style>
