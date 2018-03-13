<template>
  <div class="search">
    <h3>Type in somthing up in space</h3>
    <form v-on:submit.prevent="getResult(query)">
      <input type="text" v-model="query" />
    </form>
    <div class="results" v-if="results">

      <div v-for="result in results">
          <img v-bind:src="result.links[0].href" />
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'search',
  data () {
    return {
      msg: 'Search',
      query: '',
      results: ""
    }
  },
  methods: {
    getResult(query) {
        axios.get('https://images-api.nasa.gov/search?q=' + query + '&media_type=image').then( response => {
            console.log(response.data.collection.items);
           this.results = response.data.collection.items;    });
    }
  }
}
</script>

<style>
  reuslts img {
    height: 300px;
    margin:10px;
  }
</style>

