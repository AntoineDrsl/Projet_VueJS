<template>
    <v-container grid-list-xs>
        <v-toolbar dark color="teal">
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
            <img :src="getImgUrl(photo.name)" class="d-block w-100 pointer" :alt="photo.category" @click="overlay = index">
            <div style="width: 15%" class="fav-little pointer">
              <img :src="chooseHeart(photo)" @click="changeFav(photo)" alt="fav" class="w-100">
            </div>
            <v-overlay :value="overlay === index">
                <div style="width: 50vw">
                  <img :src="getImgUrl(photo.name)" alt="photo.category" class="w-100" @click="overlay = false">
                  <div style="width: 15%" class="fav-overlay pointer">
                    <img :src="chooseHeart(photo)" @click="changeFav(photo)" alt="fav" class="w-100">
                  </div>
                </div>
            </v-overlay>
          </div>
        </div>
        <v-snackbar
          v-model="snackbar"
          :timeout="1500"
        >
          Image ajoutée au favoris
          <v-btn
            color="blue"
            text
            @click="snackbar = false"
          >
            Close
          </v-btn>
        </v-snackbar>
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
        overlay: false,
        snackbar: false,
        categories: [
          'Animaux',
          'Paysage',
          'Nourriture',
          'Ville',
          'Femme',
          'Fantaisie'
        ],
        photos: [
          { name: 'castle.jpg', category: 'Ville', fav: false },
          { name: 'cat.jpg', category: 'Animaux', fav: false },
          { name: 'clouds.jpg', category: 'Fantaisie', fav: false },
          { name: 'elephant.jpg', category: 'Animaux', fav: false },
          { name: 'fisherman.jpg', category: 'Paysage', fav: false },
          { name: 'frog.jpg', category: 'Animaux', fav: false },
          { name: 'galaxy.jpg', category: 'Fantaisie', fav: false },
          { name: 'gallo.jpg', category: 'Animaux', fav: false },
          { name: 'girl.jpg', category: 'Femme', fav: false },
          { name: 'landscape.jpg', category: 'Paysage', fav: false },
          { name: 'moulin.jpg', category: 'Paysage', fav: false },
          { name: 'mountains.jpg', category: 'Paysage', fav: false },
          { name: 'sad.jpg', category: 'Femme', fav: false },
          { name: 'street.jpg', category: 'Ville', fav: false },
          { name: 'sunset.jpg', category: 'Paysage', fav: false },
          { name: 'tree.jpg', category: 'Paysage', fav: false },
          { name: 'woman.jpg', category: 'Femme', fav: false },
          { name: 'women.jpg', category: 'Femme', fav: false }
        ],
        favs: []
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
      changeFav: function(photo) {
        if(!photo.fav) {
          this.favs.push(photo.name)
          this.snackbar = true;
          photo.fav = true;
        } else {
          const supprIndex = this.favs.indexOf(photo.name)
          if(supprIndex > -1) {
            this.favs.splice(supprIndex, 1)
          }
          photo.fav = false;
        }
      },
      chooseHeart: function(photo) {
        if(photo.fav) {
          return require('../assets/heart-full.png')
        } else {
          return require('../assets/heart-empty.png')
        }
      }
    },
    watch: {
      search (val) {
        val && val !== this.select && this.querySelections(val)
      },
      favs : {
        handler: function() {
          window.localStorage.setItem('vue:favs', JSON.stringify(this.favs));
        },
        deep: true
      },
      photos : {
        handler: function() {
          window.localStorage.setItem('vue.photos', JSON.stringify(this.photos));
        },
        deep: true
      }
    },
    created: function() {
      this.favs = JSON.parse(window.localStorage.getItem('vue:favs') || this.favs)
      this.photos = JSON.parse(window.localStorage.getItem('vue.photos') || this.photos)
    }
}
</script>

<style>
    
</style>