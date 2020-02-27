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
            ></v-autocomplete>
        </v-toolbar>
        <div class="row mx-auto">
          <div class="col-md-4 w-100 h-100" v-for="(photo, index) of filteredPhotos" :key="index">
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
          { name: 'castle.jpg', category: 'Ville' },
          { name: 'cat.jpg', category: 'Animaux' },
          { name: 'clouds.jpg', category: 'Fantaisie' },
          { name: 'elephant.jpg', category: 'Animaux' },
          { name: 'fisherman.jpg', category: 'Paysage' },
          { name: 'frog.jpg', category: 'Animaux' },
          { name: 'galaxy.jpg', category: 'Fantaisie' },
          { name: 'gallo.jpg', category: 'Animaux' },
          { name: 'girl.jpg', category: 'Femme' },
          { name: 'landscape.jpg', category: 'Paysage' },
          { name: 'moulin.jpg', category: 'Paysage' },
          { name: 'mountains.jpg', category: 'Paysage' },
          { name: 'sad.jpg', category: 'Femme' },
          { name: 'street.jpg', category: 'Ville' },
          { name: 'sunset.jpg', category: 'Paysage' },
          { name: 'tree.jpg', category: 'Paysage' },
          { name: 'woman.jpg', category: 'Femme' },
          { name: 'women.jpg', category: 'Femme' }
        ]
      }
    },
    computed: {
      filteredPhotos: function() {
        if(!this.select) {
          return this.photos
        } else {
          return this.photos.filter(photo => photo.category === this.select);
        }
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
      }
    }
}
</script>

<style>
    
</style>