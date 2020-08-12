<template>
  <v-main>
    <v-container>
      <h1 class="text-center primary--text text-h2 mb-8">
        Feed<span class="info--text">stagram</span>
      </h1>
      <div class="wrapper justify-space-around">
        <v-card
          v-for="(cat, i) in images"
          :key="i"
          class="ma-6 p-3"
          width="460px"
          height="250px"
        >
          <div class="d-flex flex-no-wrap justify-space-between">
            <div>
              <v-card-title class="headline">{{ breeds[i].name }}</v-card-title>

              <v-card-subtitle>
                Life Span: {{ breeds[i].life_span }}
              </v-card-subtitle>
              <v-card-subtitle>
                {{ breeds[i].temperament }}
              </v-card-subtitle>
            </div>
            <v-avatar class="ma-3" size="125" tile>
              <v-img :src="cat.url"></v-img>
            </v-avatar>
          </div>
          <v-card-text>
            <v-icon large color="teal darken-2">mdi-email</v-icon>
            <a :href="breeds[i].wikipedia_url">
              {{ breeds[i].wikipedia_url }}
            </a>
          </v-card-text>
        </v-card>
      </div>
    </v-container>
  </v-main>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      images: [],
      breeds: [],
    }
  },
  created() {
    axios.defaults.headers.common['x-api-key'] = process.env.CATS_KEY
    this.loadImages()
    this.getBreeds()
  },
  methods: {
    async getBreeds() {
      try {
        const response = await axios.get('https://api.thecatapi.com/v1/breeds/')
        this.breeds = response.data
      } catch (err) {
        console.log(err)
      }
    },
    async loadImages() {
      try {
        const response = await axios.get(
          'https://api.thecatapi.com/v1/images/search',
          { params: { limit: 10, size: 'small' } }
        )

        this.images = response.data
      } catch (err) {
        console.log(err)
      }
    },
  },
}
</script>

<style>
.wrapper {
  display: flex;
  flex-wrap: wrap;
}
</style>
