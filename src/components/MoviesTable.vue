<template>
    <div>
        <h2>Movie table</h2>
        <table>
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
                <td>{{Movie.cast.join(', ')}}</td>
                <td>{{Movie.genres.join(', ')}}</td>
            </tr>
            </tbody>
        </table>
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