<template>
  <v-app>
    <v-app-bar
      dark
      extended
      fixed
      prominent
      shrink-on-scroll
      src="./assets/tree.jpg"
      scroll-threshold="200"
      color="#457DEB"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(100,115,201,.4), rgba(25,32,72,.4)"
        ></v-img>
      </template>

      <v-spacer />
      <v-toolbar-title>Lolo's Photos</v-toolbar-title>
       <v-spacer />
      <template v-slot:extension>
        <v-tabs centered>
          <v-tab @click="toAccueil">Accueil</v-tab>
          <v-tab @click="toPhotos">Mes photos</v-tab>
          <v-tab @click="toShooting">Shooting</v-tab>
          <v-tab @click="toContact">Me contacter</v-tab>
        </v-tabs>
      </template>
    </v-app-bar>

    <v-content style="margin-top: 250px">
      <accueil v-if="accueil" />
      <photos v-if="photos" />
      <shooting v-if="shooting" />
      <contact v-if="contact" />
    </v-content>
  </v-app>
</template>

<script>
import Accueil from './components/Accueil';
import Photos from './components/Photos';
import Shooting from './components/Shooting';
import Contact from './components/Contact';

export default {
  name: 'App',

  components: {
    Accueil,
    Photos,
    Shooting,
    Contact
  },

  data: () => ({
      accueil: true,
      photos: false,
      shooting: false,
      contact: false
  }),

  methods: {
    toAccueil: function() {
      if(!this.accueil) {
        this.accueil = true
        this.photos = false
        this.shooting = false
        this.contact = false
      }
    },
    toPhotos: function() {
      if(!this.photos) {
        this.accueil = false
        this.photos = true
        this.shooting = false
        this.contact = false
      }
    },
    toShooting: function() {
      if(!this.shooting) {
        this.accueil = false
        this.photos = false
        this.shooting = true
        this.contact = false
      }
    },
    toContact: function() {
      if(!this.contact) {
        this.accueil = false
        this.photos = false
        this.shooting = false
        this.contact = true
      }
    },
  }
};
</script>
