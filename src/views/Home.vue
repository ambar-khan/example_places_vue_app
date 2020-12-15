<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>Add a new place</h2>
    <p>Name:<input type='text' v-model='name'></p>
    <p>Address:<input type='text' v-model='address'></p>
    <button v-on:click="createPlace()">Add Place</button>

    <div v-for="place in places">
      {{ place.name }}
    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Places!",
      places: [],
      name: "",
      address: "",
    };
  },
  created: function () {
    console.log("in created");
    this.placesIndex();
  },
  methods: {
    placesIndex: function () {
      console.log("products index..");
      axios.get("/api/places").then((response) => {
        console.log(response.data);
        this.places = response.data;
      });
    },
    createPlace: function () {
      console.log("creating product...");
      var params = {
        name: this.name,
        address: this.address,
      };
      axios.post("/api/places", params).then((response) => {
        console.log(response.data);
        this.places.push(response.data);
      });
    },
  },
};
</script>
