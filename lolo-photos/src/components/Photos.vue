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
                label="Animal, paysage, nourriture..."
                solo-inverted
            ></v-autocomplete>
        </v-toolbar>
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
          'Femme'
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
      }
    }
}
</script>

<style>
    
</style>