<template>
    <div id="movie-filter">
        <div>Filter Results</div>
        <h3>By time of day</h3>
        <div class="filter-group">
            <check-filter v-for="time in times" category="time" :title="time" :key="time" v-on:check-filter="checkFilter"></check-filter>
        </div>
        <h3>By Genre</h3>
        <div class="filter-group">
            <check-filter v-for="genre in genres" category="genre" :title="genre" :key="genre" v-on:check-filter="checkFilter"></check-filter>
        </div>
    </div>
</template>
<script>
    import genres from '../util/genres';
    import times from '../util/times';
    import CheckFilter from './CheckFilter.vue'
    export default {
        data:function () {
            return {
                genres,
                times
            }
        },
        methods:{
            checkFilter (category,title,checked) {
                this.$emit('check-filter',category,title,checked);
            }
        },
        components:{
            CheckFilter
        }
    }
</script>