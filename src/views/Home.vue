<template>
  <div class="content">
    <component :is="current"></component>
    <div class="calltoaction">
      <v-btn id="cta" elevation="2" dark fab text @click="toggleComponent">{{ btext }}</v-btn>
    </div>
  </div>
</template>

<script>
import CharacterCard from '../components/CharacterCard.vue'
import PlanetCard from '../components/PlanetCard.vue'

export default {
  name: 'Home',

  components: {
    CharacterCard,
    PlanetCard

  },
  data () {
    return {
      current: 'character-card',
      btext: 'Character'
    }
  },
  methods: {
    toggleComponent () {
      if (this.current === 'planet-card') {
        this.current = 'character-card'
        this.btext = 'Characters'
      } else {
        this.current = 'planet-card'
        this.btext = 'Planets'
      }
    }
  }
}
</script>
