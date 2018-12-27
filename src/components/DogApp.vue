<template>
    <v-container >
        <v-layout row wrap class="justify-center" >
            <v-flex lg6 md6>
                <v-select  append-icon label="Select Breed" :items="breeds"   @change="onSelectBreed"/>

                <v-select  append-icon label="Select Optional Sub Breed" :items="subbreeds" @change="onSelectSubbreed" />
            </v-flex>

        </v-layout>

        <v-layout row wrap class="justify-center">
            <v-flex lg6 md6>

            <v-carousel dark >
                    <v-carousel-item
                            v-for="(img,i) in images"
                            :key="i"
                            :src="img.src"
                    >
                    </v-carousel-item>
                </v-carousel>


            </v-flex>

        </v-layout>

    </v-container>


</template>

<script>
    export default {
        name: "DogApp",
        data: () => ({
            breeds: [],
            subbreeds: [],
            allBreeds: [],
            images: [],
            selected: {
                breed: null,
                subbreed: null
            }
        }),
    mounted: async function(){
           const response = await fetch('https://dog.ceo/api/breeds/list/all');
           const allBreeds = await response.json();

           this.breeds = Object.keys(allBreeds.message).map(key => {
               return {
                   'text': key,
                   'value': key
               };
           });
           this.allBreeds = allBreeds.message;


        },

    methods: {
        onSelectBreed: function(value){
            this.resetSelectedBreeds();
            this.subbreeds = this.allBreeds[value];
            this.selected.breed = value;
            this.loadImages();
        },
        onSelectSubbreed: function(value) {
            this.selected.subbreed = value;
            this.loadImages();
        },
        loadImages: async function(){

            const url = (this.selected.subbreed) ? `https://dog.ceo/api/breed/${this.selected.breed}/${this.selected.subbreed}/images` : `https://dog.ceo/api/breed/${this.selected.breed}/images`;
            const response = await fetch(url);
            const images = await response.json();
            this.images = images.message.map(url => {
                return {
                   src: url
                    }
               }

            )
        },
        resetSelectedBreeds: function(){
            this.selected.breed = null;
            this.selected.subbreed = null;
        }
    }
    }
</script>

<style scoped>

</style>