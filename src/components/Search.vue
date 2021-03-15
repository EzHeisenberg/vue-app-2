<template>
  <div class="container">
    <h1 class="text-center">Rechercher une catégorie</h1>
    <form>
      <div class="input-group mb-3 w-75 mx-auto">
        <input type="text" class="form-control border-dark" v-model="searchNews" placeholder="Entrer votre recherche"/>
        <button type="submit" @click="newsSearch" class="btn btn-outline-dark">rechercher</button>
        <button type="button" data-bs-toggle="modal" data-bs-target="#exampleModal" class="btn btn-outline-dark">
          Catégories
        </button>
      </div>
    </form>

    <div class="row">
      <div class="col-md-6" :v-model="News" v-for="(dataNews, index) in News" :key="index+1">
        <div class="card border-secondary mb-3">
          <b class="card-header">#{{ index + 1 }} - {{ dataNews.title }}</b>
          <div class="card-body">
            <p>{{ dataNews.description }}</p>
            <p>- {{ dataNews.author }}</p>
            <p>Catégorie :
              <span v-for="(dataCategorie) in dataNews.category" :key="dataCategorie">{{ dataCategorie }} </span>
            </p>
            <div class="d-flex justify-content-end">
              <router-link :to="{ name: 'Article', params: { id: index }}" class="btn btn-outline-dark">Voir l'article
              </router-link>
              <a :href="dataNews.url" class="btn btn-outline-dark">aller sur le site</a>
            </div>
          </div>
        </div>
      </div>
    </div>
    <hr>

    <div class="d-flex justify-content-end">
      <p>total d'articles : {{ News.length }}</p>
    </div>



    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog modal-lg modal-dialog-centered modal-dialog-scrollable">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Catégories</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <div class="grid-container">
              <div class="btn btn-outline-dark" data-bs-dismiss="modal" @click="go_to(cat)" v-for="(cat) in Categories" :key="cat">{{ cat }}</div>
            </div>
          </div>
        </div>
      </div>
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
      Categories: [],
    };
  },
  created() {
    this.categorie()
  },
  methods: {
    newsSearch: async function () {
      try {
        const response = await axios.get(apiURL + this.searchNews.toLowerCase());
        console.log(response)
        this.News = response.data.news;
      } catch (error) {
        console.log(error);
      }
    },
    categorie: async function () {
      try {
        const response = await axios.get('https://api.currentsapi.services/v1/available/categories');
        this.Categories = response.data.categories;
      } catch (error) {
        console.log(error);
      }
    },
    go_to: function (c) {
      this.searchNews = c;
      console.log(c)
      console.log(this.searchNews)
      this.newsSearch();
    },
    openNav: function () {
      document.getElementById("myNav").style.height = "100%";

    },
    closeNav: function () {
      document.getElementById("myNav").style.height = "0%";

    }

  }
}


</script>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: auto auto auto;
  grid-gap: 10px;
}

.grid-container > div {
  text-align: center;
}


@media (max-width: 594px) {
  .grid-container {
    display: grid;
    grid-template-columns: auto auto;
    grid-gap: 10px;
  }
}
</style>