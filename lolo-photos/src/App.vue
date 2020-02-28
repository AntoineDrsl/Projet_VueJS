<template>
  <v-app id="background">
    <v-app-bar
      dark
      extended
      fixed
      prominent
      shrink-on-scroll
      src="./assets/tree.jpg"
      scroll-threshold="200"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(100,115,201,.4), rgba(25,32,72,.4)"
        ></v-img>
      </template>

      <v-spacer />
      <v-toolbar-title class="h1" id="main-title">Lolo's Photos</v-toolbar-title>
       <v-spacer />
      <template v-slot:extension>
        <v-tabs centered>
          <v-tab @click="toPhotos">Mes photos</v-tab>
          <v-tab @click="toLikes">Vos likes</v-tab>
          <v-tab @click="toPixelart">Créer son pixelArt</v-tab>
        </v-tabs>
      </template>
    </v-app-bar>

    <v-content style="margin-top: 250px">
      <photos v-if="photos" />
      <likes v-if="likes" />
      <pixelart v-if="pixelart" />
    </v-content>
  </v-app>
</template>

<script>
import Photos from './components/Photos';
import Likes from './components/Likes';
import Pixelart from './components/Pixelart';

export default {
  name: 'App',

  components: {
    Photos,
    Likes,
    Pixelart
  },

  data: () => ({
      photos: true,
      likes: false,
      pixelart: false
  }),

  methods: {
    toPhotos: function() {
      if(!this.photos) {
        this.photos = true
        this.likes = false
        this.pixelart = false
      }
    },
    toLikes: function() {
      if(!this.likes) {
        this.photos = false
        this.likes = true
        this.pixelart = false
      }
    },
    toPixelart: function() {
      if(!this.pixelart) {
        this.photos = false
        this.likes = false
        this.pixelart = true
      }
    },
  }
};
</script>
