<template>
    <v-container>
        <div class="row">
            <div class="col-md-8">
                <div id="canvas">
                    <div v-for="(pixel, index) in 90" :key="index" id="pixel"></div>
                </div>
            </div>
            <div class="col-md-4">
                <v-color-picker v-model="selectedColor"></v-color-picker>
            </div>
        </div>
    </v-container>
</template>

<script>
export default {
    name: 'pixelart',
    data () {
        return {
            selectedColor: ''
        }
    }
}
</script>

<style>
    
</style>