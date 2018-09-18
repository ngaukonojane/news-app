<template>
  <div class="container">

    <h1>News</h1>

    <input v-model="search" type="text" name="search" placeholder="Search..">
    <button v-on:click="loadNews" type="button">Search</button>
    


    <p v-if="loading">Please wait...</p>
    <i class="fa fa-circle-o-notch fa-spin" style="font-size:24px"></i>
    <div v-for="article in news">
      
      
      <img :src="article.urlToImage" alt="">

      <h3>{{article.title}} </h3>

      <h4>{{article.author}}</h4>

      <a class="button" :href="article.url" target="_blank">Read more</a>

    </div>

  </div>
</template>


<script>

import axios from 'axios'

const baseUrl = "https:newsapi.org/v2";
const apikey = "201ccf08fc5a4577aff5a20bae86a3fa";
const endpoint = "/everything";

const data = {
  news: [],
  search:'',
  loading:false
}



export default {
  data: function() {
    return data 
  },

  created() {
    this.loadNews();
  },

  methods: {
      loadNews() {
        if(this.search.length < 1) {
          return;
        }

        this.loading=true;

        this.news = [];

      let url = baseUrl + endpoint + '?q=' + this.search + '&apikey=' + apikey;

      localStorage.setItem('list')



      axios.get(url).then(function(response) {
        console.log(response.data.articles)
        data.loading=false;
        data.news = response.data.articles
        
        
      }).catch(function(error) {
          console.log(error.message)
      })
    }
  }
}
</script>