<template>
  <v-main>
    <v-container v-if="breeds.length">
      <h1 class="text-center primary--text text-h1 mb-8">
        Feed<span class="info--text font-weight-black">stagram</span>
      </h1>
      <div class="wrapper justify-space-around">
        <v-card
          v-for="(cat, i) in images"
          :key="i"
          class="my-4 mx-2 p-3 card"
          color="orange lighten-5"
          width="460px"
          height="250px"
        >
          <div class="d-flex flex-no-wrap justify-space-between">
            <div>
              <v-card-title class="headline">{{ breeds[i].name }}</v-card-title>

              <v-card-subtitle>
                Life Span: {{ breeds[i].life_span }} years
              </v-card-subtitle>
              <v-card-subtitle>
                {{ breeds[i].temperament }}
              </v-card-subtitle>
            </div>
            <v-avatar class="ma-3" size="150">
              <v-img :src="cat.url"></v-img>
            </v-avatar>
          </div>
          <v-card-text>
            <v-icon
              class="mail"
              color="green lighten-2"
              title="Cats aint got no mail meow"
              >mdi-email</v-icon
            >
            <a :href="breeds[i].wikipedia_url" target="_blank">
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
  async created() {
    axios.defaults.headers.common['x-api-key'] = process.env.CATS_KEY
    await this.loadImages()
    await this.getBreeds()
  },
  methods: {
    async getBreeds() {
      try {
        const response = await axios.get('https://api.thecatapi.com/v1/breeds/')
        this.breeds = response.data
      } catch (err) {
        // eslint-disable-next-line no-console
        console.error(err)
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
        // eslint-disable-next-line no-console
        console.error(err)
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
.mail {
  cursor: pointer;
}
@media (max-width: 1263px) {
  .card {
    flex-grow: 1;
    flex-shrink: 1;
    max-width: 50vw;
  }
}
</style>
