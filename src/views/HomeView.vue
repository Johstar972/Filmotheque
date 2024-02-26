<template>
  <div>
    <movieSearch @searchMovieEmit="setMovieSearch"/>
    <MovieDetail v-if="movieId != null" :movieId="movieId" :buttonIsClicked="buttonClicked" @buttonIsClicked="hiddenMovieDetail"/>
    <MovieList @showMovieDetailEmit="this.addId" @button-clicked="this.handleButtonClicked" :textField="textField"/>
  </div>
  
</template>

<script>
import MovieList from '@/components/MovieList.vue';
import MovieDetail from '@/components/MovieDetail.vue';
import movieSearch from '@/components/movieSearch.vue';
import MoviePagination from '@/components/MoviePagination.vue';
export default {
  name: 'HomeView',
  components: {
    MovieList,
    MovieDetail,
    movieSearch,
    MoviePagination
  },
  data(){
    return {
      movieId:null,
      buttonClicked:false,
      textField:''
    }
  },
  methods: {
    addId(movie)
    {
      
      this.movieId = movie;
      console.log(movie)
    },

    handleButtonClicked(value)
    {
      this.buttonClicked = value;
      console.log(this.buttonClicked)
    },

    hiddenMovieDetail(value)
    {
      if (value === true){
        this.buttonClicked = false;
        this.movieId = null;
      }
        
    },

    setMovieSearch(value)
    {
      this.textField = value;
    }
  }
}

</script>
