<template>
    <div id="app">
        <div class="container">
            <h1>Baza filmów</h1>
            <MoviesTable :Movies="Movies"/>
            <GenresList :SlicedMovies="SlicedMovies" :SlicedGenres="SlicedGenres"/>
        </div>
    </div>
</template>

<script>
    import axios from "axios";
    // import Movies from './assets/movies.json'
    import MoviesTable from "@/components/MoviesTable";
    import GenresList from "@/components/GenresList";
    import underscore from "underscore"

    export default {
        name: 'app',
        components: {GenresList, MoviesTable},
        created() {
            axios.get('/movies.json').then(response => {
                this.Movies = response.data;
                this.SlicedMovies = this.Movies.slice(28600, 28700);
                this.prepGenres();
                // eslint-disable-next-line no-console
                console.log(this.Movies)
            })
        },
        data() {
            return {
                Movies: [],
                SlicedMovies: [],
                SlicedGenres: []
            }
        },
        methods: {
            prepGenres() {
                let temp = [];
                underscore.each(this.SlicedMovies, function (Movie) {
                    temp.push(Movie.genres)
                });
                temp = underscore.flatten(temp);
                this.SlicedGenres = underscore.uniq(temp);
                // eslint-disable-next-line no-console
                console.log(this.SlicedGenres)
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
