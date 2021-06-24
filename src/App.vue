<template>
  <v-app>
    <v-main>
      <v-app-bar dark>
        <v-toolbar-title>Star Wars Character API</v-toolbar-title>
      </v-app-bar>
        <router-view/>
        <Footer />
    </v-main>
  </v-app>
</template>

<script>
import './assets/global.scss'
import Footer from './components/Footer.vue'
export default {
  components: { Footer },
  name: 'App',

  data: () => ({
    //
  })
}
</script>
