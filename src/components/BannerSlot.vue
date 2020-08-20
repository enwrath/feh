<template>
  <div class="bannerHero" v-bind:class="hero.color" v-on:click="showDetails = !showDetails" >
    <img v-if="!showDetails || !('season' in hero)" v-bind:src="`./images/${hero.name}.webp`" />

    <HeroDetails v-if="showDetails && 'season' in hero" v-bind:hero="hero" />

  </div>
</template>

<script>
import HeroDetails from '@/components/HeroDetails.vue'

export default {
  name: 'BannerSlot',
  components: {
    HeroDetails
  },
  props: {
    hero: {}
  },
  data() {
    return {
      showDetails: false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.Red {
  background-color: #f78484;
}
.Blue {
  background-color: #afd5ff;
}
.Green {
  background-color: #94f194;
}
.Colorless {
  background-color: #8080807a;
}
.bannerHero {
  display: inline-block;
}
img {
  max-width: 100%;
  background-color: #ffffff69;
  border-style: solid;
  border-width: thick;
  box-sizing: border-box;
}
</style>
