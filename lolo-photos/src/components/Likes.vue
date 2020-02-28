<template>
    <v-container>
        <v-carousel hide-delimiter-background show-arrows-on-hover delimiter-icon="mdi-minus" v-if="favs.length > 0">
            <v-carousel-item v-for="(fav, index) in favs" :key="index" :src="getFavUrl(fav)"></v-carousel-item>
        </v-carousel>
        <div v-else>Vous n'avez liké aucune image pour le moment :(</div>
    </v-container>
</template>

<script>
export default {
    name: 'likes',
    data() {
        return {
            favs: []
        }
    },
    methods: {
        getFavUrl(fav) {
            return require('../assets/' + fav)
        }
    },
    created: function() {
      this.favs = JSON.parse(window.localStorage.getItem('vue:favs') || this.favs)
    }
}
</script>

<style>
    
</style>