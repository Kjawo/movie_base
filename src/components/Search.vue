<template>
    <form>
        <div class="form-group">
            <label for=inputTitle>Tytuł</label>
            <input v-model="SearchTitle" type="text" id=inputTitle class="form-control"
                   placeholder="Podaj tytuł lub fragment tytułu filmu"/>
        </div>
        <div class="form-group row">
            <label class="col-sm-4 col-form-label" for="inputProductionFrom">Rok produkcji od:</label>
            <div class="col-sm-8">
                <input v-model="StartYear" type="text" id=inputProductionFrom class="form-control"
                       placeholder="Liczba naturalna z przedziału 1900-2019"/>
            </div>
        </div>
        <div class="form-group row">
            <label class="col-sm-4 col-form-label" for="inputProductionTo">Rok produkcji do:</label>
            <div class="col-sm-8">
                <input v-model="EndYear" type="text" id=inputProductionTo class="form-control"
                       placeholder="Liczba naturalna z przedziału 1900-2019"/>
            </div>
        </div>
        <div class="form-group">
            <label for="inputCast">Obsada</label>
            <input v-model="SearchCast" type="text" id="inputCast" class="form-control" placeholder="Imię i nazwisko"/>
        </div>
        <div class="form-group row">
            <input @click="filterMovies" type="button" class="btn btn-info col-sm-12" value="Szukaj"/>
        </div>
    </form>
</template>

<script>

    import underscore from "underscore";

    export default {
        name: "Search",
        props: ['Movies'],
        data() {
            return {
                SearchTitle: '',
                StartYear: '',
                EndYear: '',
                SearchCast: '',
            }
        },
        methods: {
            filterMovies() {
                let filteredMovies = this.Movies;
                let tmpSearchTitle = this.SearchTitle;
                let tmpStartYear = this.StartYear;
                let tmpEndYear = this.EndYear;
                let tmpSearchCast = this.SearchCast;

                filteredMovies = underscore.filter(filteredMovies, function (movie) {
                    return movie.title.includes(tmpSearchTitle)
                });

                if (tmpStartYear !== "") {
                    filteredMovies = underscore.filter(filteredMovies, function (movie) {
                        return movie.year >= Number(tmpStartYear)
                    });
                }

                if (tmpEndYear !== "") {
                    filteredMovies = underscore.filter(filteredMovies, function (movie) {
                        return movie.year <= Number(tmpEndYear)
                    });
                }

                filteredMovies = underscore.filter(filteredMovies, function (movie) {
                    return movie.cast.join(' ').includes(tmpSearchCast)
                });

                this.$emit('newFilteredMovies', {filteredMovies})
            }
        }
    }
</script>

<style scoped>

</style>