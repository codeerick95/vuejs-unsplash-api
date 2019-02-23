<template>
  <div id="app" class="container">
    <div class="row mb-5">
      <div class="col-md-6 offset-md-3 text-center">
        <img alt="Vue logo" src="./assets/logo.png" class="vue-logo" />
        <img
          alt="Vue logo"
          src="./assets/unsplash-logo.jpg"
          class="unsplash-logo"
        />
        <p class="mb-5">
          Un pequeño ejemplo de como consumir la Api de
          <a href="https://unsplash.com/">Unsplash</a>
          con el paquete oficial
          <a href="https://github.com/unsplash/unsplash-js">unsplash-js</a>
          y por supuesto aprovechando lo mejor de
          <a href="https://vuejs.org/">Vuejs</a>.
        </p>
        <p class="text-muted">
          Busca alguna foto instantáneamente, por ejemplo: team, nature, etc...
        </p>
        <div class="form-group">
          <form @submit.prevent="getPhotos()">
            <input
              type="text"
              placeholder="Buscar imagen"
              class="form-control"
              v-model="query"
            />
          </form>
        </div>
      </div>
    </div>
    <div class="card-columns">
      <Card v-for="photo in photos" :key="photo.id" :photo="photo" />
    </div>
  </div>
</template>

<script>
import Unsplash from "unsplash-js";
import Card from "./components/Card.vue";

export default {
  name: "app",
  components: {
    Card
  },
  data() {
    return {
      query: "",
      page: 1,
      photos: []
    };
  },
  watch: {
    query() {
      this.getPhotos();
    }
  },
  methods: {
    getPhotos() {
      const unsplash = new Unsplash({
        applicationId:
          "Tú applicationId de Unsplash / your Unsplash applicationId",
        secret:
          "Tú secret de Unsplash"
      });
      unsplash.search
        .photos(this.query, this.page, 10)
        .then(toJson => {
          return toJson.json();
        })
        .then(json => {
          this.photos = json.results;
        });
    }
  }
};
</script>

<style lang="scss">
.vue-logo {
  max-width: 50px;
}

.unsplash-logo {
  max-width: 150px;
}

.icon {
  max-width: 25px;
}

.form-control {
  box-shadow: none !important;
}
</style>
