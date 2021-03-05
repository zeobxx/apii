<template>
  <div>
    <div class="v-application">
      <v-text-field v-model="query" label="Search"></v-text-field>
      <v-btn class="ma-2" outlined color="black" @click="SearchManga">
        Search
      </v-btn>
    </div>
    <v-divider class="mt-4 mb-4"></v-divider>
    <div class="d-flex flex-wrap">
      <v-card
        v-for="manga in results"
        :key="manga.id"
        class="ma-5"
        max-width="344"
        @click="handleMangaClick(manga)"

      >
        <v-card-text
          ><h5>ID : {{ manga.mal_id }}</h5></v-card-text
        >

        <v-img
          :src="manga.image_url"
          width="400"
          height="400px"
          @click="handleMangaClick(mangas)"
        ></v-img>

        <v-card-title> {{ manga.title }} </v-card-title>
        <v-card-subtitle>
          <v-rating
            :value="manga.score"
            color="amber"
            dense
            half-increments
            length="10"
            readonly
            size="14"
          ></v-rating
          >score : {{ manga.score }} <br />Start date : {{ manga.start_date }}
          <br />end date : {{ manga.end_date }}</v-card-subtitle
        >
        <v-divider></v-divider>

        <v-card-text>
          <h3>{{ manga.synopsis }}</h3>
          <!-- <h4 @click="uu">{{ manga.url }}</h4> -->
        </v-card-text>
      </v-card>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      query: '',
      results: [],
      show: false,
    }
  },
  methods: {
    SearchManga() {
      const url = `https://api.jikan.moe/v3/search/manga?q=${this.query}&page=1/`
      axios.get(url).then((res) => {
        console.log(res.data)
        this.results = res.data.results
      })
    },
    handleMangaClick(mangas) {
      console.log('MANGA', mangas)
      window.location = manga.url
    },
  },
}
</script>

<style>
.theme--dark.v-application {
  background: #81967c;
  color: #fce7e7;
}

v-application .text {
  color: #140404 !important;
  caret-color: #070707 !important;
}
</style>
