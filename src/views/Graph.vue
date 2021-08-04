<template>
  <div class="graph">
    <h1>{{ message }}</h1>
    <div>
      <button v-on:click="toggleVue = !toggleVue">Show Vue Data</button>
      <div v-show="toggleVue">
        <p>Forks: {{ this.vueData.forks }}</p>
        <p>Subscribers: {{ this.vueData.subscribers_count }}</p>
        <p>Watchers: {{ this.vueData.watchers_count }}</p>
      </div>
    </div>
    <div>
      <button v-on:click="toggleAngular = !toggleAngular">
        Show Angular Data
      </button>
      <div v-show="toggleAngular">
        <p>Forks: {{ this.angularData.forks }}</p>
        <p>Subscribers: {{ this.angularData.subscribers_count }}</p>
        <p>Watchers: {{ this.angularData.watchers_count }}</p>
      </div>
    </div>
    <div>
      <button v-on:click="toggleEmber = !toggleEmber">Show Ember Data</button>
      <div v-show="toggleEmber">
        <p>Forks: {{ this.emberData.forks }}</p>
        <p>Subscribers: {{ this.emberData.subscribers_count }}</p>
        <p>Watchers: {{ this.emberData.watchers_count }}</p>
      </div>
    </div>
    <div>
      <button v-on:click="toggleSvelte = !toggleSvelte">
        Show Svelte Data
      </button>
      <div v-show="toggleSvelte">
        <p>Forks: {{ this.svelteData.forks }}</p>
        <p>Subscribers: {{ this.svelteData.subscribers_count }}</p>
        <p>Watchers: {{ this.svelteData.watchers_count }}</p>
      </div>
    </div>
    <div>
      <button v-on:click="toggleReact = !toggleReact">Show React Data</button>
      <div v-show="toggleReact">
        <p>Forks: {{ this.reactData.forks }}</p>
        <p>Subscribers: {{ this.reactData.subscribers_count }}</p>
        <p>Watchers: {{ this.reactData.watchers_count }}</p>
      </div>
    </div>
    <bar-chart></bar-chart>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import BarChart from "./BarChart.vue";

export default {
  components: { BarChart },
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      vueData: {},
      angularData: {},
      emberData: {},
      svelteData: {},
      reactData: {},
      toggleVue: false,
      toggleAngular: false,
      toggleEmber: false,
      toggleSvelte: false,
      toggleReact: false,
    };
  },
  created: function () {
    this.getVueData();
    this.getAngularData();
    this.getEmberData();
    this.getSvelteData();
    this.getReactData();
  },
  methods: {
    getVueData: function () {
      fetch("https://api.github.com/repos/vuejs/vue")
        .then((response) => response.json())
        .then((data) => {
          this.vueData = data;
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
          this.emberData = response.data;
        })
        .catch((error) => console.log(error.response.data.errors));
    },

    getSvelteData: function () {
      axios
        .get("https://api.github.com/repos/sveltejs/svelte")
        .then((response) => {
          this.svelteData = response.data;
        });
    },

    getReactData: function () {
      fetch("https://api.github.com/repos/facebook/react")
        .then((response) => response.json())
        .then((data) => {
          this.reactData = data;
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
