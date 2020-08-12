<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <v-container class="text-center">
        <v-row>
          <v-col>
            <h1>Welcome to Catstagram</h1>
            <h3>The app your cat has been itching for!</h3>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <p>
              Please go
              <nuxt-link to="login">here to login</nuxt-link>, or
              <nuxt-link to="feed"> here to see the Feed</nuxt-link>.
            </p>
          </v-col>
        </v-row>
      </v-container>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  components: {},
}
</script>
