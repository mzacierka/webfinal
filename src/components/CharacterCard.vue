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
              <li>Name: {{ this.character.character_name }}</li>
              <li>Height: {{ this.character.height }}</li>
              <li>Hair Color: {{ this.character.hair_color }}</li>
              <li>Skin Color: {{ this.character.skin_color }}</li>
              <li>Eye Color: {{ this.character.eye_color }}</li>
              <li>Birth Year: {{ this.character.birth_year }}</li>
              <li>Gender: {{ this.character.gender }}</li>
              <li>Home World: {{ this.character.homeworld }}</li>
            </ul>
          </div>
          <v-btn id="submitbtn" dark @click="getCharacterName" width="100%" height="40px">Click Me</v-btn>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'
export default {
  name: 'CharacterCard',

  data () {
    return {
      character: {
        id: 1,
        character_name: 'Luke Skywalker',
        height: '172',
        hair_color: 'blond',
        skin_color: 'fair',
        eye_color: 'blue',
        birth_year: '18BBY',
        gender: 'male',
        homeworld: 'Tatooine'
      },
      imagesource: ''
    }
  },
  methods: {
    async getCharacterName () {
      var num = Math.floor(Math.random() * 30) + 1
      if (num === 17) num = 5

      const resp = await axios.get(`https://www.swapi.tech/api/people/${num}`)
      const results = resp.data.result.properties
      const homeworldresp = await axios.get(results.homeworld)
      const homew = homeworldresp.data.result.properties.name
      this.character.character_name = results.name
      this.character.height = results.height
      this.character.hair_color = results.hair_color
      this.character.skin_color = results.skin_color
      this.character.eye_color = results.eye_color
      this.character.birth_year = results.birth_year
      this.character.gender = results.gender
      this.character.homeworld = homew
      this.character.id = num
      this.imagesource = require('../assets/characters/' + this.character.id + '.jpg')
    }
  },
  mounted () {
    this.imagesource = require('../assets/characters/1.jpg')
  }
}
</script>
