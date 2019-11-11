<template>
    <div id="app">
        <div class="container">
            <h1>Baza filmów</h1>
            <MoviesTable :Movies="Movies"/>
        </div>
    </div>
</template>

<script>

    import axios from "axios";
    // import Movies from './assets/movies.json'
    import MoviesTable from "@/components/MoviesTable";

    export default {
        name: 'app',
        components: {MoviesTable},
        created() {
            axios.get('/movies.json').then(response => {
                this.Movies = response.data;
                // eslint-disable-next-line no-console
                console.log(this.Movies)
            })
        },
        data () {
            return {
                Movies: []
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
