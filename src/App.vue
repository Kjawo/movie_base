<template>
    <div id="app">
        <div class="container">
            <h1>Baza filmów</h1>
            <Search :Movies="Movies" @newFilteredMovies="updateFilteredMovies"/>
            <MoviesTable :Movies="FilteredMovies" />
            <GenresList :SlicedMovies="SlicedMovies" :SlicedGenres="SlicedGenres"/>
            <CastList :SlicedMovies="SlicedMovies" :SlicedCast="SlicedCast"/>
        </div>
    </div>
</template>

<script>
    import axios from "axios";
    // import Movies from './assets/movies.json'
    import underscore from "underscore"

    import MoviesTable from "@/components/MoviesTable";
    import GenresList from "@/components/GenresList";
    import CastList from "@/components/CastList";
    import Search from "@/components/Search";

    export default {
        name: 'app',
        components: {Search, GenresList, MoviesTable, CastList},
        created() {
            axios.get('/movies.json').then(response => {
                this.Movies = response.data;
                this.FilteredMovies = this.Movies;
                this.SlicedMovies = this.Movies.slice(28600, 28700);
                this.prepSlicedData();
                // eslint-disable-next-line no-console
                console.log(this.Movies)
            })
        },
        data() {
            return {
                Movies: [],
                FilteredMovies: [],
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
            },
            updateFilteredMovies(payload) {
                this.FilteredMovies = payload.filteredMovies;
                // eslint-disable-next-line no-console
                console.log(payload.filteredMovies);
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
