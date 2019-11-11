<template>
    <div id="app">
        <div class="container">
            <h1>Baza filmów</h1>
            <MoviesTable :Movies="Movies"/>
            <GenresList :SlicedMovies="SlicedMovies" :SlicedGenres="SlicedGenres"/>
            <CastList :SlicedMovies="SlicedMovies" :SlicedCast="SlicedCast"/>
        </div>
    </div>
</template>

<script>
    import axios from "axios";
    // import Movies from './assets/movies.json'
    import MoviesTable from "@/components/MoviesTable";
    import GenresList from "@/components/GenresList";
    import CastList from "@/components/CastList";
    import underscore from "underscore"

    export default {
        name: 'app',
        components: {GenresList, MoviesTable, CastList},
        created() {
            axios.get('/movies.json').then(response => {
                this.Movies = response.data;
                this.SlicedMovies = this.Movies.slice(28600, 28700);
                this.prepSlicedData();
                // eslint-disable-next-line no-console
                console.log(this.Movies)
            })
        },
        data() {
            return {
                Movies: [],
                SlicedMovies: [],
                SlicedGenres: [],
                SlicedCast: []
            }
        },
        methods: {
            prepSlicedData() {
                let tempGenre = [];
                let tempCast = [];
                underscore.each(this.SlicedMovies, function (Movie) {
                    tempGenre.push(Movie.genres);
                    tempCast.push(Movie.cast)

                });
                tempGenre = underscore.flatten(tempGenre);
                tempCast = underscore.flatten(tempCast);
                this.SlicedGenres = underscore.uniq(tempGenre);
                this.SlicedCast = underscore.uniq(tempCast);
                // eslint-disable-next-line no-console
                console.log(this.SlicedCast)
            }
        },

        // mounted(){
        //   // eslint-disable-next-line no-console
        //     console.log(Movies)
        // }
    }
</script>

<style>
    /*#app {*/
    /*    font-family: 'Avenir', Helvetica, Arial, sans-serif;*/
    /*    -webkit-font-smoothing: antialiased;*/
    /*    -moz-osx-font-smoothing: grayscale;*/
    /*    text-align: center;*/
    /*    color: #2c3e50;*/
    /*    margin-top: 60px;*/
    /*}*/
</style>
