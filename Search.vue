<template>
  <main>
    <div class="container-fluid pb-5" id="main-container">
      <div class="row mt-5">
        <div class="offset-lg-4 col form-inline">
          <input
            type="text"
            class="form-control col-md-4 col-8"
            v-model="searchQuery"
            placeholder="Buscar"
            @keyup.enter="search"
          />
          <button class="btn btn-success" @click="search">Buscar</button>
          <button class="btn btn-danger">X</button>
        </div>
        <div class="offset-lg-4 col-md-4 text-left pt-1">
          <p>
            <small>Encontrados: {{ encontrados }}</small>
          </p>
        </div>
      </div>
      <PmNotification v-show="showNotification">
        <div
          class="alert"
          :class="{
            'alert-danger': showResults,
            'alert-success': !showResults
          }"
          slot="body"
        >
          <p v-if="showResults">No se encontraron resultados</p>
          <p v-else>Se encontraron: {{ encontrados }} resultados</p>
        </div>
      </PmNotification>
      <PmLoader v-show="isLoading" />
      <div class="row mt-3">
        <div class="col-md-3 mb-4" v-for="t in tracks">
          <PmTrack
            :class="{ isActive: t.id === setSelectedTrack }"
            :track="t"
            @select="selectedTrack"
            v-blur="t.preview_url"
          />
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import trackService from "../services/track";

import PmTrack from "./track";

import PmLoader from "./shared/Loader";
import PmNotification from "./shared/Notification";

export default {
  name: "App",
  data() {
    return {
      searchQuery: "",
      tracks: [],
      isLoading: false,
      setSelectedTrack: "",
      showNotification: false,
      showResults: true
    };
  },
  methods: {
    search() {
      if (!this.searchQuery) {
        return;
      }
      this.isLoading = true;
      trackService.search(this.searchQuery).then(res => {
        this.showNotification = res.tracks.total >= 0;
        this.showResults = res.tracks.total === 0;
        this.tracks = res.tracks.items;
        this.isLoading = false;
      });
    },
    selectedTrack(id) {
      this.setSelectedTrack = id;
      console.log(id);
    }
  },
  computed: {
    encontrados() {
      return this.tracks.length;
    }
  },
  watch: {
    showNotification() {
      if (this.showNotification) {
        setTimeout(() => {
          this.showNotification = false;
        }, 3000);
      }
    }
  },
  components: {
    PmTrack,
    PmLoader,
    PmNotification
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.search  {
  height: 20px;
  font-size: 5em;
}
#lista-artistas li {
  list-style: none;
}
.isActive {
  border: 2px #167bff solid;
}
#main-container {
  min-height: 100vh;
}
</style>
