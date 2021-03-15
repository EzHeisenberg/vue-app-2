<template>
  <div class="container">
    <h1 class="text-center">Rechercher une catégorie</h1>
    <form>
      <div class="input-group mb-3 w-75 mx-auto">
        <input type="text" class="form-control border-dark" v-model="searchNews" placeholder="Entrer votre recherche"/>
        <button type="submit" @click="newsSearch" class="btn btn-outline-dark">rechercher</button>
      </div>
    </form>
    {{searchNews.toLowerCase()}}


    <div class="row">
      <div class="col-md-6" v-for="(dataNews, index) in News" :key="dataNews.length">
        <div class="card border-secondary mb-3">
          <b class="card-header">#{{ index }} - {{ dataNews.title }}</b>
          <div class="card-body">
            <p>{{ dataNews.description }}</p>
            <p>- {{ dataNews.author }}</p>
            <div class="d-flex justify-content-end">
              <router-link :to="{ name: 'Article', params: { id: index }}" class="btn btn-outline-dark">Voir l'article
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
    <hr>
    <div class="d-flex justify-content-end">
      <p>total d'articles : {{ News.length }}</p>
    </div>


  </div>
</template>

<script>

import * as axios from "axios";

const apiKey = 'apiKey=7Dtcv7fjRjOKXcmEZvI5_UMUuOSWjzqtwoUXvNhPqA0pR66U'

const apiURL = 'https://api.currentsapi.services/v1/search?language=fr&'
    + apiKey + '&category=';


export default {
  name: "Search",

  data: function () {
    return {
      searchNews: "",
      News: [],
    };
  },
  methods: {
    newsSearch: async function () {
      try {
        const response = await axios.get(apiURL + this.searchNews.toLowerCase());
        this.News = response.data.news;
      } catch (error) {
        console.log(error);
      }
    },
  }
}
</script>

<style scoped>

</style>