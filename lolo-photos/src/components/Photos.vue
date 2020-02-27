<template>
    <v-container grid-list-xs>
        <v-toolbar
            dark
            color="teal"
        >
            <v-toolbar-title>Cherchez une photo</v-toolbar-title>
            <v-autocomplete
                v-model="select"
                :loading="loading"
                :items="items"
                :search-input.sync="search"
                cache-items
                class="mx-3"
                flat
                hide-no-data
                hide-details
                label="Animaux, paysage, nourriture..."
                solo-inverted
                @keydown="show()"
            ></v-autocomplete>
        </v-toolbar>
        <div class="row mx-auto">
          <div class="col-md-4 w-100 h-100" v-for="(photo, index) of photos" :key="index">
            <img :src="getImgUrl(photo.name)" class="d-block w-100" :alt="photo.category">
          </div>
        </div>
    </v-container>
</template>

<script>
export default {
    name: 'photos',
    data () {
      return {
        loading: false,
        items: [],
        search: null,
        select: null,
        categories: [
          'Animaux',
          'Paysage',
          'Nourriture',
          'Ville',
          'Femme',
          'Fantaisie'
        ],
        photos: [
          { name: 'castle.jpg', category: 'ville' },
          { name: 'cat.jpg', category: 'animaux' },
          { name: 'clouds.jpg', category: 'fantaisie' },
          { name: 'elephant.jpg', category: 'animaux' },
          { name: 'fisherman.jpg', category: 'paysage' },
          { name: 'frog.jpg', category: 'animaux' },
          { name: 'galaxy.jpg', category: 'fantaisie' },
          { name: 'gallo.jpg', category: 'animaux' },
          { name: 'girl.jpg', category: 'femme' },
          { name: 'landscape.jpg', category: 'paysage' },
          { name: 'moulin.jpg', category: 'paysage' },
          { name: 'mountains.jpg', category: 'paysage' },
          { name: 'sad.jpg', category: 'femme' },
          { name: 'street.jpg', category: 'ville' },
          { name: 'sunset.jpg', category: 'paysage' },
          { name: 'tree.jpg', category: 'paysage' },
          { name: 'woman.jpg', category: 'femme' },
          { name: 'women.jpg', category: 'femme' }
        ]
      }
    },
    watch: {
      search (val) {
        val && val !== this.select && this.querySelections(val)
      }
    },
    methods: {
      querySelections (v) {
        this.loading = true
        setTimeout(() => {
          this.items = this.categories.filter(e => {
            return (e || '').toLowerCase().indexOf((v || '').toLowerCase()) > -1
          })
          this.loading = false
        }, 500)
      },
      getImgUrl: function(photo) {
        return require('../assets/' + photo)
      },
      show: function() {
        console.log(this.select)
      }
    }
}
</script>

<style>
    
</style>