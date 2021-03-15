<template>
  <div class="container">
    <h3 class="text-center">{{ Article.title }}</h3>
    <hr>
    <div class="row">
      <div class="col-md-6">
        <img :src="Article.image" alt="" class="img-fluid">
      </div>
      <div class="col-md-6">
        <p>{{ Article.description }}</p>
        <hr>

        <p>Catégorie :
          <span v-for="(dataArticle) in Article.category" :key="dataArticle">{{ dataArticle }} </span>
        </p>
        <p>Publier le : {{ Article.published }}</p>
        <p>Auteur : {{ Article.author }}</p>
        <div class="d-flex justify-content-end">
          <a :href="Article.url" class="btn btn-outline-dark">Voir sur le site</a>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import * as axios from "axios";

const apiKey = 'apiKey=7Dtcv7fjRjOKXcmEZvI5_UMUuOSWjzqtwoUXvNhPqA0pR66U'

const apiURL = 'https://api.currentsapi.services/v1/latest-news?' +
    'language=fr&' + apiKey;

export default {
  name: "Artc",
  data: function () {
    return {
      Article: [
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

    };
  },
  created: function () {
    this.Articlefr()
  },
  methods: {
    Articlefr: async function () {
      try {
        const response = await axios.get(apiURL)
        this.Article = response.data.news[this.$route.params.id];
      } catch (error) {
        console.log(error);
      }
    }
  },
}
</script>