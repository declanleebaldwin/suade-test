<template>
    <div class="card" v-show="person.name">
        <div class="card-content">
            <p class="title is-4">{{ person.name }}</p>
            <p>Age: {{ person.age }}</p>
            <p>Eye Colour: {{ person.eyeColor }}</p>
            <p>Gender: {{ person.gender }}</p>
            <p>Location</p>
            <p class="margin-left">Latitude: {{ person.location.latitude }}</p>
            <p class="margin-left">Longitude: {{ person.location.longitude }}</p>
            <p>Preferences</p>
            <p class="margin-left">Pet: {{ person.preferences.pet }}</p>
            <p class="margin-left">Fruit: {{ person.preferences.fruit }}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: "SelectedPerson",
    props: {
        person: {}
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.margin-left {
    margin-left: 1rem;
}
</style>
