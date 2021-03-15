<template>
  <div class="container">
    <h1 class="text-center">News de France</h1>
    <p>Date : {{ currentDay }}</p>
    <form>
      <div class="input-group mb-3 w-75 mx-auto">
        <select class="form-select" v-model="langage" @change="lang($event)">
          <option value="fr">Français</option>
          <option value="en">English</option>
          <option value="de">German</option>
          <option value="it">Italy</option>
        </select>
      </div>
    </form>

    <hr>
    <div class="row">
      <div class="col-md-6" v-for="(dataNews, index) in News" :key="dataNews.length">
        <div class="card border-secondary mb-3">
          <b class="card-header">#{{ index+1 }} - {{ dataNews.title }}</b>
          <div class="card-body">
            <p>{{ dataNews.description }}</p>
            <p>- {{ dataNews.author }}</p>
            <p>Catégorie :
              <span v-for="(dataCategorie) in dataNews.category" :key="dataCategorie">{{ dataCategorie }} </span>
            </p>
            <div class="d-flex justify-content-end">
              <router-link :to="{ name: 'Article', params: { id: index }}" class="btn btn-outline-dark">Voir l'article
              </router-link>
            </div>
          </div>
        </div>
      </div>
      <div class="d-flex justify-content-end">
        <p>total d'articles : {{ News.length }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import * as axios from "axios";
import * as moment from "moment";

const apiKey = 'apiKey=7Dtcv7fjRjOKXcmEZvI5_UMUuOSWjzqtwoUXvNhPqA0pR66U'

export default {
  name: "News",
  data: function () {
    return {
      currentDay: moment().format('DD-MM-YYYY'),
      News: [
        {
          id: "",
          title: "",
          description: "",
          url: "",
          image: "",
          language: "",
          category: [],
          published: "",
        }
      ],
      langage: "fr",
    };
  },
  created: function () {
    this.Newsfr()
  },
  methods: {
    lang(event) {
      this.langage = event.target.value;
      this.Newsfr();
    },
    Newsfr: async function () {
      try {
        const response = await axios.get('https://api.currentsapi.services/v1/latest-news?' + 'language=' + this.langage + '&' + apiKey);
        this.News = response.data.news;
      } catch (error) {
        console.log(error);
      }
    }
  }
}
</script>

<style>

</style>