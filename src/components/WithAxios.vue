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
      <div class="card border-0" v-for="photo in photos" :key="photo.id">
        <img :src="photo.urls.regular" alt="Demo" class="img-fluid" />
        <div
          class="card-img-overlay d-flex justify-content-between align-items-start"
        >
          <template v-if="photo">
            <div>
              <img
                :src="photo.user.profile_image.small"
                alt="User profile image"
                class="rounded-circle"
              />
              <a href class="btn btn-link text-white">
                {{ photo.user.username }}
              </a>
            </div>
            <span class="badge badge-light align-self-end">
              <img src="./assets/like.png" alt="Icon like" class="icon" />
              {{ photo.likes }}
            </span>
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const axios = require("axios");

export default {
  name: "app",
  data() {
    return {
      query: "",
      client_id:
        "617ced32bb237bddc6b510a81c810c5f881079f7a3092b647b8162b17c3bddef",
      page: 1,
      per_page: 10,
      photos: []
    };
  },
  watch: {
    query(val) {
      this.query = val;
      axios
        .get(
          `https://api.unsplash.com/search/photos?query=${this.query}&page=${
            this.page
          }&per_page=${this.per_page}&client_id=${this.client_id}`
        )
        .then(response => {
          this.photos = response.data.results;
        })
        .catch(error => {
          console.log(error);
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
