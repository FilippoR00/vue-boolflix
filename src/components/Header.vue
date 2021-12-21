<template>
	<div>
		<div class="left">
			<img src="..\assets\logo.png" alt="Logo">
			<ul>
				<li><a href="#">Home</a></li>
				<li><a href="#">Serie TV</a></li>
				<li><a href="#">Film</a></li>
				<li><a href="#">Originali</a></li>
				<li><a href="#">Aggiunto di recente</a></li>
				<li><a href="#">La mia lista</a></li>
			</ul>
		</div>
		<div class="right">
			<div class="search">
				<input type="text" v-model="search" v-on:keyup.enter="getMovies" placeholder="Cerca...">
				<button @click='getMovies'><i class="fas fa-search"></i></button>
			</div>
			<div class='kids'><a href="#">BAMBINI</a></div>
			<div class="notify"><i class="fas fa-bell"></i><i class="fas fa-exclamation-circle"></i></div>
			<div class="user">
				<img src="https://upload.wikimedia.org/wikipedia/commons/0/0b/Netflix-avatar.png" alt="User Logo">
				<i class="fas fa-chevron-down"></i>
			</div>
		</div>
	</div>
</template>

<script>
import axios from 'axios';
import dataShared from "../share/dataShared";

export default {
	name: 'Header',
	data() {
		return {
			search : 'spider man',
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
				dataShared.myMovie = response.data.results;
			})
			.catch(function (error) {
				console.log(error);
			});

			axios.get('https://api.themoviedb.org/3/search/tv', {
				params: {
					api_key : '0b9ac5d0a41cb0ca49e6d38df58bc461',
					language : 'it-IT',
					query : this.search
				}
			})
			.then(function (response) {
				dataShared.myTV = response.data.results;
			})
			.catch(function (error) {
				console.log(error);
			});  
		},
		
	},
	mounted() {
		this.getMovies();
		this.search = '';
	}
}
</script>

<style scoped lang="scss">
	@import "../style/Global.scss";
	div{
		display: flex;
		justify-content: space-between;
		.left{
			display: flex;
			align-items: center;
			img{
			width: 150px;
			margin: 10px 20px;
			}
			ul{
				display: flex;
				li{
					list-style: none;
					padding: 0px 5px;
					a{
						color: white;
						text-decoration: none;
						padding: 5px;
					}
				}
			}
		}
		.right{
			display: flex;
			align-items: center;
			.search{
				input{
					border: none;
					border-radius: 20px;
					outline: none;
					background-color: #333;
					padding: 0px 20px;
					color: lightgray;
					width: 100px;
					transition: 0.3s;
				}
				input:focus{
						width: 200px;
						color: white;
				}
				button{
					border: none;
					border-radius: 50%;
					padding: 7px 9px;
					margin: 0px 10px;
					background-color: $mainColor;
					color: white;
					cursor: pointer;
					font-size: 20px;
				}
				button:hover{
					background-color: #333;
				}
			}
			.kids{
				a{
					color: white;
					text-decoration: none;
				}
			}
			.notify{
				position: relative;
				svg:first-child{
					font-size: 20px;
					margin: 0px 10px;
					cursor: pointer;
				}
				svg:last-child{
					color: red;
					width: 10px;
					position: absolute;
					right: 9px;
					bottom: 5px;
				}
			}
			.user{
				display: flex;
				align-items: center;
				img{
					height: 30px;
					padding: 0px 10px;
					cursor: pointer;
				}
				svg{
					font-size: 10px;
					margin-right: 20px;
					cursor: pointer;
				}
			}
		}
	}
</style>
