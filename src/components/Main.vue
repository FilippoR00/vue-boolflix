<template>
    <div>
        <div class="row-title">Movies:</div>
        <div class="row">
            <div class="movies" v-for="(movie, index) in dataShared.myMovie" :key="index">
                <div class="img-container">
                    <img :src="printImg(movie.poster_path)" :alt="movie.original_title + ' image'">
                    <div class="card-info">
                        <div class="title"><strong>TITOLO</strong> : {{movie.title}}</div>
                        <div class="original-title" v-if="movie.title != movie.original_title"><strong>TITOLO ORIGINALE:</strong> {{movie.original_title}}</div>
                        <div class="language"><strong>LINGUA:</strong>  {{langFlag(movie.original_language) + movie.original_language}}</div>
                        <div class="rating"><strong>VOTO:</strong> {{movie.vote_average }} <span class="star" v-html='rating(movie.vote_average)'></span></div>
                    </div>
                </div>
            </div>
            <div class="content" v-if="dataShared.MovieContent">La ricerca non ha prodotto risultati</div>
        </div>
        <div class="row-title">Serie TV:</div>
        <div class="row">
            <div class="tv-series" v-for="(tv, index) in dataShared.myTV" :key="dataShared.myMovie.length + index">
                <div class="img-container">
                    <img :src="printImg(tv.poster_path)" :alt="tv.original_name + ' image'">
                    <div class="card-info">
                        <div class="card-info">
                            <div class="title"><strong>TITOLO:</strong> {{tv.name}}</div>
                            <div class="original-title" v-if="tv.name != tv.original_name"><strong>TITOLO ORIGINALE:</strong> {{tv.original_name}}</div>
                            <div class="language"><strong>LINGUA:</strong>  {{langFlag(tv.original_language) + tv.original_language}}</div>
                            <div class="rating"><strong>VOTO:</strong> {{tv.vote_average }} <span class="star" v-html='rating(tv.vote_average)'></span></div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="content" v-if="dataShared.TVcontent">La ricerca non ha prodotto risultati</div>
        </div>
    </div>
</template>

<script>
import dataShared from "../share/dataShared";

export default {
    name: 'Main',
    data() {
        return {
            dataShared,
        }
    },
    methods: {
        langFlag(val) {
			switch (val) {
				case "it":
					return '🇮🇹 ';
                case "en":
                    return '🇺🇸 ';
                case "ja":
					return '🇯🇵 ';
                case "uk":
                    return '🇬🇧 ';
                case "de":
					return '🇩🇪 ';
                case "fr":
                    return '🇫🇷 ';
                case "da":
                    return '🇩🇰 ';
                case "nl":
                    return '🇳🇱 ';
                case "es":
                    return '🇪🇸 ';
                case "pl":
                    return '🇵🇱 ';
                case "ca":
                    return '🇨🇦 ';
				default:
					return '🏳️‍🌈 ';
			}
		},
        printImg(val) {
            if (val != null) {
                return 'https://image.tmdb.org/t/p/' + 'w300/' + val;
            }
            else {
                return 'https://elementarchitects.com/wp-content/uploads/2021/08/1200px-No-Image-Placeholder.svg.png';
            }
        },
        rating(val) {
            let temp = Math.ceil(val / 2);
            return `<i class="fas fa-star"></i>`.repeat(temp);
        },
    },
}
</script>

<style scoped lang="scss">
	@import "../style/Global.scss";
    .row-title{
        font-size: 30px;
        margin: 10px 25px;
    }
    .row{
        min-height: 350px;
        max-width: 100vw;
        overflow-x: scroll;
        padding: 25px;
        margin-bottom: 30px;
        display: flex;
        column-gap: 25px;
        .img-container{
            position: relative;
            cursor: pointer;
            img{
                width: 300px;
                height: 450px;
                object-fit: cover;
                border-radius: 20px;
            }
            .card-info{
                overflow: hidden;
                position: absolute;
                top: 0px;
                left: 0px;
                border-radius: 20px;
                background-color: black;
                height: 100%;
                width: 100%;
                opacity: 0;
                transition: 0.2s;
                padding: 20px;
                .title{
                    font-size: 25px;
                    margin-bottom: 30px;
                }
                div{
                    margin: 10px 0px;
                    font-size: 20px;
                    .star{
                        color: rgb(255, 217, 0);
                    }
                }
            }
            
        }
        .card-info:hover{
            opacity: 0.85;
        }
        .content{
            width: 100%;
            font-size: 25px;
            text-align: center;
        }
    }
</style>
