<template>
  <v-app>
    <v-app-bar fixed app class="primary">
      <nuxt-link to="/">
        <v-btn color="info">CatsTagram</v-btn>
      </nuxt-link>
      <nuxt-link to="login" class="ml-4">
        <v-btn color="success">Login</v-btn>
      </nuxt-link>
      <nuxt-link to="feed" class="ml-4">
        <v-btn color="warning">Feed</v-btn>
      </nuxt-link>
      <v-spacer />
      <v-btn icon>
        <v-icon>mdi-menu</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-footer absolute app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      fixed: false,
      right: true,
      title: 'The Catstagram',
    }
  },
}
</script>

<style scoped>
#logo {
  background-color: #ffcc00;
  padding: 5px;
  cursor: pointer;
  text-decoration: none;
}
</style>
