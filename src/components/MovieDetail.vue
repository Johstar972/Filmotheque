<template>
    
        <v-dialog :model-value="buttonIsClicked" @update:model-value="buttonIsClicked = $event" width="800" persistent>
            <v-card>
                
                
                <div class="d-flex flex-column align-center">
                    <v-card-title class="text-center">
                        {{ movie.title }}
                    </v-card-title>
                    <v-img v-if="movie.poster_path" :src="picture+movie.poster_path" width="300" height="300"/>
                </div>
                
                <v-card-text>
                    Production:
                    <div class="d-flex flex-wrap justify-space-between">
                        <div v-for="companie in companies" class="mr-2 mb-2">
                            <v-img v-if="companie.logo_path" :src="picture+companie.logo_path" width="100" height="100"></v-img>
                        </div>
                    </div>
                </v-card-text>

                <v-card-text>
                    Résumé: 
                    <div>{{ movie.overview }}</div>
                </v-card-text>

                <v-btn v-on:click="closeDetail()">Fermer</v-btn>
                
            </v-card>
        </v-dialog>
    
</template>
<script>

import axios from 'axios';
const config = require("/src/config.json")

export default {
    name: 'movieDetail',
    props : ['movieId','buttonIsClicked'],

    data(){
        return {
            movie: {},
            picture: config.url.photo_path,
            companies: [],
            
        }
        
    },

    methods:{
        closeDetail(){
            this.$emit('buttonIsClicked',true);
        }
    },
    mounted() {
        axios.get(config.url.movie_detail + this.movieId, {
            headers: {
            'Authorization': `bearer ${config.api_key}`
            }
        })
        .then((res) => {
        this.movie = res.data;
        this.companies = res.data.production_companies;
        console.log(res.data.production_companies);
        
        })
        .catch((error) => {
        console.error(error);
        });
    },

    

}

</script>