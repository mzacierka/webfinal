<template>
  <v-container>
    <v-row align="center" justify="center" id="contentrow">
      <v-col>
        <v-img :src="imagesource" height="500px" width="500px"></v-img>
      </v-col>
      <v-col>
        <div class="card">
          <div class="characterlist">
            <ul id="demographics">
              <li>Name: {{ this.planet.planet_name }}</li>
              <li>Diameter: {{ this.planet.diameter }}</li>
              <li>Rotation Period: {{ this.planet.rotation_period }}</li>
              <li>Orbital Period: {{ this.planet.orbital_period }}</li>
              <li>Gravity: {{ this.planet.gravity }}</li>
              <li>Population: {{ this.planet.population }}</li>
              <li>Climate: {{ this.planet.climate }}</li>
              <li>Terrain: {{ this.planet.terrain }}</li>
            </ul>
          </div>
          <v-btn id="submitbtn" dark @click="getPlanetName" width="100%" height="40px">Click Me</v-btn>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'
export default {
  name: 'PlanetCard',
  data () {
    return {
      planet: {
        id: 1,
        planet_name: 'Tatooine',
        diameter: '10465',
        rotation_period: '23',
        orbital_period: '304',
        gravity: '1 standard',
        population: '200000',
        climate: 'arid',
        terrain: 'desert'
      },
      imagesource: ''
    }
  },
  methods: {
    async getPlanetName () {
      var num = Math.floor(Math.random() * 3) + 1
      if (num === 17) num = 5

      const resp = await axios.get(`https://www.swapi.tech/api/planets/${num}`)
      const results = resp.data.result.properties
      this.planet.planet_name = results.name
      this.planet.diameter = results.diameter
      this.planet.rotation_period = results.rotation_period
      this.planet.orbital_period = results.orbital_period
      this.planet.gravity = results.gravity
      this.planet.population = results.population
      this.planet.climate = results.climate
      this.planet.terrain = results.terrain
      this.planet.id = num
      this.imagesource = require('../assets/planets/' + this.planet.id + '.jpg')
    }
  },
  mounted () {
    this.imagesource = require('../assets/planets/1.jpg')
  }
}
</script>
