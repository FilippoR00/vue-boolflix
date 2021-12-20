<template>
    <div>
        <div>Movies:</div>
        <div class="movies" v-for="(movie, index) in dataShared.myMovie" :key="index">
            <div class="title">TITOLO: {{movie.title}}</div>
            <div class="original-title">TITOLO ORIGINALE: {{movie.original_title}}</div>
            <div class="language">LINGUA:  {{langFlag(movie.original_language) + movie.original_language}}</div>
            <div class="rating">VOTO: {{movie.vote_average}}</div>
        </div>
        <div>Serie TV:</div>
        <div class="tv-series" v-for="(data, index) in dataShared.myTV" :key="index">
            <div class="title">TITOLO: {{data.name}}</div>
            <div class="original-title">TITOLO ORIGINALE: {{data.original_name}}</div>
            <div class="language">LINGUA:  {{langFlag(data.original_language) + data.original_language}}</div>
            <div class="rating">VOTO: {{data.vote_average}}</div>
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
				default:
					return '🏳️‍🌈';
			}
		}
    },
}
</script>

<style scoped lang="scss">

</style>
