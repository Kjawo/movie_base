<template>
    <div>
        <h2>Movie table</h2>
        <table class="responsive-table">
            <thead>
            <tr>
                <th>Title</th>
                <th>Production Year</th>
                <th>Cast</th>
                <th>Genres</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(Movie, index) in lessMovieTable" v-bind:key="index">
                <td>"{{Movie.title}}"</td>
                <td>{{Movie.year}}</td>
                <td>{{Movie.cast}}</td>
                <td>{{Movie.genres}}</td>
            </tr>
            </tbody>
        </table>
        <button @click="showMore">Show more</button>
        <a @click="showMore" class="btn-floating btn-large waves-effect waves-light red"><i class="material-icons">add</i></a>
    </div>
</template>

<script>

    export default {
        name: "MoviesTable",
        props: ['Movies'],
        data() {
            return {
                showNumber: 10
            }
        },
        methods: {
            showMore() {
                this.showNumber += 10
            }

        },
        computed: {
            lessMovieTable() {
                return this.Movies.slice(0, this.showNumber)
            }
        }
    }

</script>

<style>

</style>