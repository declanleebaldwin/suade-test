<template>
    <div id="app">
        <section class="hero is-primary">
            <div class="hero-body">
                <div class="container">
                    <h1 class="title">
                        Suade Front End Challenge 2019
                    </h1>
                    <h2 class="subtitle">
                        Declan Baldwin
                    </h2>
                </div>
            </div>
        </section>
        <section class="search-section">
            <div class="container">
                <div class="columns">
                    <div class="column is-half">
                        <h4 class="title is-4">Select a person for details.</h4>
                        <input
                            class="input"
                            type="text"
                            placeholder="Search for a person here."
                            v-model="searchText"
                        />
                        <button class="button is-success" @click="searchPeople()">
                          Search
                        </button>
                    </div>
                </div>
            </div>
        </section>
        <section class="people-section">
            <div class="container">
                <div class="columns">
                    <div class="column">
                        <div class="list is-hoverable">
                            <a
                                class="list-item"
                                v-for="person in visiblePeople"
                                v-bind:key="person.id"
                                @click="selectedPerson = person"
                            >
                                {{ person.name }}
                            </a>
                        </div>
                    </div>
                    <div class="column">
                        <selected-person
                            :person="selectedPerson"
                        ></selected-person>
                    </div>
                </div>
            </div>
        </section>
        <section class="pagination">
            <div class="container">
                <div class="columns">
                    <div class="column is-half">
                        <nav
                            class="pagination"
                            role="navigation"
                            aria-label="pagination"
                        >
                            <button
                                class="pagination-previous"
                                type="button"
                                title="This is the first page"
                                @click="updatePage(currentPage - 1)"
                                :disabled="currentPage == 0"
                            >
                                Previous
                            </button>
                            <button
                                class="pagination-next"
                                type="button"
                                @click="updatePage(currentPage + 1)"
                                :disabled="currentPage == numberOfPages - 1"
                            >
                                Next page
                            </button>
                            <ul class="pagination-list">
                                <li
                                    v-for="(pageNumber, index) in numberOfPages"
                                    v-bind:key="index"
                                >
                                    <a
                                        class="pagination-link"
                                        :class="{
                                            'is-current': index == currentPage
                                        }"
                                        @click="updatePage(index)"
                                        >{{ pageNumber }}</a
                                    >
                                </li>
                            </ul>
                        </nav>
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>

<script>
import SelectedPerson from "./components/SelectedPerson.vue";
import peopleData from "./assets/people.json";

export default {
    name: "app",
    components: {
        SelectedPerson
    },
    data() {
        return {
            people: peopleData,
            selectedPerson: {},
            currentPage: 0,
            pageSize: 10,
            visiblePeople: [],
            searchText: '',
            filterPeople: peopleData
        };
    },
    methods: {
        searchPeople() {
            var $this = this;
            this.filterPeople = this.people.filter(function(person) {
                return (
                    person.name
                        .toLowerCase()
                        .indexOf($this.searchText.toLowerCase()) !== -1
                );
            });
            this.updatePage(0);

        },
        updateVisiblePeople() {
            this.visiblePeople = this.filterPeople.slice(
                this.currentPage * this.pageSize,
                this.currentPage * this.pageSize + this.pageSize
            );
        },
        updatePage(pageNumber) {
            this.currentPage = pageNumber;
            this.updateVisiblePeople();
        }
    },
    computed: {
        numberOfPages() {
            return Math.ceil(this.filterPeople.length / this.pageSize);
        }
    },
    mounted() {
        this.updateVisiblePeople();
    }
};
</script>

<style>
</style>
