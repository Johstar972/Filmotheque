<template>
    <v-row>
        <v-col cols="3" v-for="movie in movieFiltered" :key="movie.id">
            <v-card height="550" width="400">
                <v-card-title class="text-center" >
                    {{ movie.title }}
                </v-card-title>
                <div class="d-flex flex-column align-center">
                    <v-img :src="pictures + movie.poster_path" width="400" height="400"/>
                    
                </div>
                <div class="mt-10 d-flex flex-column align-center">
                    <v-btn v-on:click="SendMovie(movie)">Plus d'informations</v-btn>
                </div>
            </v-card>
        </v-col>        
    </v-row>

   
</template>
<script>

import axios from 'axios';
import _ from 'lodash';

const config = require("/src/config.json")

export default {
    name: 'MoviesList', 
    props: ['textField'],
    
    data(){
        return {movies: [],
                pictures: config.url.photo_path,
                
            }
    },

    methods:{
        SendMovie(movie){
            //console.log(movie)
            this.$emit("showMovieDetailEmit",movie.id)
            this.$emit("button-clicked",true)
        }
    },

    computed:{
        movieFiltered(){
            if(this.textField.trim() === '')
                return this.movies;
            else{
                
                return _.filter(this.movies, movie => {
                    return movie.title.toLowerCase().includes(this.textField.toLowerCase());
                });
            }
        }
    },
    mounted() {
        axios.get(config.url.movie_list, {
            headers: {
            'Authorization': `bearer ${config.api_key}`
            }
        })
        .then((res) => {
        this.movies = res.data.results;
        //console.log(res.data);
        })
        .catch((error) => {
        console.error(error);
        });
    },
}





</script>