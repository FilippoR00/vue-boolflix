<template>
    <div>
        <div>Movies:</div>
        <div class="movies" v-for="(movie, index) in dataShared.myMovie" :key="index">
            <img :src="printImg(movie.poster_path)" :alt="movie.original_title + ' image'">
            <div class="title">TITOLO: {{movie.title}}</div>
            <div class="original-title">TITOLO ORIGINALE: {{movie.original_title}}</div>
            <div class="language">LINGUA:  {{langFlag(movie.original_language) + movie.original_language}}</div>
            <div class="rating">VOTO: {{movie.vote_average }} <span v-html='rating(movie.vote_average)'></span></div>
        </div>
        <div>Serie TV:</div>
        <div class="tv-series" v-for="(tv, index) in dataShared.myTV" :key="dataShared.myMovie.length + index">
            <img :src="printImg(tv.poster_path)" :alt="tv.original_name + ' image'">
            <div class="title">TITOLO: {{tv.name}}</div>
            <div class="original-title">TITOLO ORIGINALE: {{tv.original_name}}</div>
            <div class="language">LINGUA:  {{langFlag(tv.original_language) + tv.original_language}}</div>
            <div class="rating">VOTO: {{tv.vote_average }} <span v-html='rating(tv.vote_average)'></span></div>
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
					return '🇮🇹';
                case "en":
                    return '🇺🇸';
                case "ja":
					return '🇯🇵';
                case "uk":
                    return '🇬🇧';
                case "de":
					return '🇩🇪';
                case "fr":
                    return '🇫🇷';
                case "da":
                    return '🇩🇰';
                case "nl":
                    return '🇳🇱';
                case "es":
                    return '🇪🇸';
                case "pl":
                    return '🇵🇱';
                case "ca":
                    return '🇨🇦';
				default:
					return '🏳️‍🌈';
			}
		},
        printImg(val) {
            if (val != null) {
                return 'https://image.tmdb.org/t/p/' + 'w300/' + val;
            }
            else {
                return 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTJ2jGheLn_aLV34b2Kfqba1DwKWlyYbaN_aev3d1mH_GHZ9FZevDjSSqs0HweHifHmHfY&usqp=CAU';
            }
        },
        rating(val) {
            let temp = Math.ceil(val / 2);
            return `<i class="fas fa-star"></i>`.repeat(temp);
        }
    },
}
</script>

<style scoped lang="scss">

</style>
