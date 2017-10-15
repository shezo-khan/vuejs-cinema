<template>

    <div id="movie-list">
        <div v-if="filteredMovies.length">
            <movie-item v-for="movie in filteredMovies"
                        :movie="movie.movie"
                        :sessions="movie.sessions"
                        :day="day"
            ></movie-item>
        </div>
        <div v-else-if="movies.length">
            No results
        </div>
        <div v-else>
            Loading
        </div>
    </div>
</template>
<script>
    import genres from '../util/genres';
    import times from '../util/times';
    import MovieItem from './MovieItem.vue';
    export default {
        data () {
            return{
            }
        },
        methods:{
            MoviePassesGenreFilter(movie){
                if(this.genre.length == 0){
                    return true;
                }else{
                    let movieGenre = movie.movie.Genre.split(", ");
                    let matched = true;
                    this.genre.forEach(genre =>{
                       if(movieGenre.indexOf(genre)===-1){
                         matched=false;
                       }
                    });
                    return matched;
                }
            },
            sessionPassesTimeFilter(session){
                if(!this.day.isSame(this.$moment(session.time),'day')){
                    return false;
                } else if(this.time.length ===0 || this.time.length === 2){
                    return true;
                } else if (this.time[0] == times.AFTER_6PM){
                    return this.$moment(session.time).hour() >=18;
                } else{
                    return this.$moment(session.time).hour() < 18;
                }
                return true;
            }
        },
        computed:{
            filteredMovies(){
                return this.movies
                    .filter(this.MoviePassesGenreFilter)
                    .filter(movie => movie.sessions.find(this.sessionPassesTimeFilter));
            }
        },
        components:{
            MovieItem
        },
        props:[
            'genre',
            'time',
            'movies',
            'day'
        ]
    }
</script>