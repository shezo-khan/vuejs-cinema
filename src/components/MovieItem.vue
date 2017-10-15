<template>
    <div class="movie">
        <div class="movie-col-left">
            <img v-bind:src="movie.Poster">
        </div>
        <div class="movie-col-right">
            <div class="movie-title">
                <h2>{{movie.Title}}</h2>
                <span class="movie-rating">{{movie.Rated}}</span>
            </div>
            <div class="movie-sessions">
                <div v-for="session in filterSessions(sessions)" class="session-time-wrapper">
                    <div class="session-time">{{formatSessionTime(session.time)}}</div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        data () {
            return{
            }
        },
        methods:{
            formatSessionTime(raw){
                return this.$moment(raw).format('h:mm A');
            },
            filterSessions(sessions){
                return sessions.filter(session =>{
                    return this.$moment(session.time).isSame(this.day, 'day');
                });
            }
        },
        computed:{

        },
        props:[
            'movie',
            'sessions',
            'day'
        ]
    }
</script>