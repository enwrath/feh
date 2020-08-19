<template>
  <div class="bannerHero" v-bind:class="hero.color" >
    <v-popover :disabled="!('season' in hero)" placement="auto">
      <!-- This will be the popover target (for the events and position) -->
      <img v-bind:src="`./images/${hero.name}.webp`" />

      <!-- This will be the content of the popover -->
      <template slot="popover">
        <HeroDetails v-bind:hero="hero" />
      </template>
    </v-popover>

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
  padding: 0.5em 0;
}
img {
  max-width: 100%;
  height: auto;
  background-color: #ffffff69;
  border-style: solid;
  border-width: thick;
  box-sizing: border-box;
}
</style>
