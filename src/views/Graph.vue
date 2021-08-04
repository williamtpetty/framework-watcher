<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <button v-on:click="getVueData()">Get Vue Data</button>
    <br />
    <button v-on:click="getAngularData()">Get Angular Data</button>
    <br />
    <button v-on:click="getEmberData()">Get Ember Data</button>
    <br />
    <button v-on:click="getSvelteData()">Get Svelte Data</button>
    <br />
    <button v-on:click="getReactData()">Get React Data</button>
    <br />
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      vueData: {},
      angularData: {},
      emberData: {},
      svelteData: {},
      reactData: {},
    };
  },
  created: function () {},
  methods: {
    getVueData: function () {
      fetch("https://api.github.com/repos/vuejs/vue")
        .then((response) => response.json())
        .then((data) => {
          this.vueData = data;
          console.log(this.vueData.forks_count);
          console.log(this.vueData.subscribers_count);
          console.log(this.vueData.watchers_count);
        })
        .catch((error) => {
          console.error(
            "There has been a problem with your fetch operation:",
            error
          );
        });
    },

    getAngularData: function () {
      fetch("https://api.github.com/repos/angular/angular.js")
        .then((response) => response.json())
        .then((data) => {
          this.angularData = data;
          console.log(this.angularData.forks_count);
          console.log(this.angularData.subscribers_count);
          console.log(this.angularData.watchers_count);
        })
        .catch((error) => {
          console.error(
            "There has been a problem with your fetch operation:",
            error
          );
        });
    },

    getEmberData: function () {
      axios
        .get("https://api.github.com/repos/emberjs/ember.js")
        .then((response) => {
          console.log(response.data.forks_count);
          console.log(response.data.subscribers_count);
          console.log(response.data.watchers_count);
          this.emberData = response.data;
        })
        .catch((error) => console.log(error.response.data.errors));
    },

    getSvelteData: function () {
      axios
        .get("https://api.github.com/repos/sveltejs/svelte")
        .then((response) => {
          console.log(response.data.forks_count);
          console.log(response.data.subscribers_count);
          console.log(response.data.watchers_count);
          this.svelteData = response.data;
        });
    },

    getReactData: function () {
      fetch("https://api.github.com/repos/facebook/react")
        .then((response) => response.json())
        .then((data) => {
          this.reactData = data;
          console.log(this.reactData.forks_count);
          console.log(this.reactData.subscribers_count);
          console.log(this.reactData.watchers_count);
        })
        .catch((error) => {
          console.log(
            "There has been a problem with your fetch operation:",
            error
          );
        });
    },
  },
};
</script>
