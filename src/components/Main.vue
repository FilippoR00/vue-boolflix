<template>
    <div>
        <div v-for="(datas, index) in dataShared.myData" :key="index">
            <div class="title">TITOLO: {{datas.title}}</div>
            <div class="original-title">TITOLO ORIGINALE: {{datas.original_title}}</div>
            <div class="language">LINGUA: {{datas.original_language}}</div>
            <div class="rating">VOTO: {{datas.vote_average}}</div>
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
}
</script>

<style scoped lang="scss">

</style>
