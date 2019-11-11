<template>
    <div>
        <h2>Cast List</h2>
        <div>
            <v-select v-model="selected"
                      :options="SlicedCast"
                      @input="filterMovies"
            ></v-select>
        </div>
        <ol>
            <!--            <li v-for="(Movie, index) in SlicedMovies" v-bind:key="index"> {{Movie.title}}</li>-->
            <li v-for="(Movie, index) in filteredMovies" v-bind:key="index"> {{Movie.title}}</li>
        </ol>

    </div>
</template>

<script>
    import vSelect from 'vue-select'
    import underscore from "underscore"


    import 'vue-select/dist/vue-select.css';


    export default {
        name: "CastList",
        props: ['SlicedMovies', 'SlicedCast'],
        data() {
            return {
                selected: '',
                filteredMovies: []
            }
        },
        methods: {
            filterMovies() {
                let tmp = this.selected;
                this.filteredMovies = underscore.filter(this.SlicedMovies, function (movie) {
                    return underscore.contains(movie.cast, tmp)
                });
            }
        },
        components: {
            vSelect
        },
        computed: {

        }

    }
</script>

<style>

</style>