<template>
  <div>
    <h2>{{banner.title}}</h2>
    <div class="bannerHeroes">
      <BannerSlot v-bind:key="`${i}-${hero}`" v-for="(hero, i) in banner.heroes" v-bind:hero="heroes[hero]" />
    </div>
  </div>
</template>

<script>
import BannerSlot from '@/components/BannerSlot.vue'

export default {
  name: 'Banner',
  components: {
    BannerSlot
  },
  props: {
    banner: {},
    heroes: {}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bannerHeroes {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  margin:auto;
  font-size: x-small;
  max-width: 400px;
}
@media only screen and (min-width: 400px) {
  .bannerHeroes {
    font-size: small;
  }
}
@media only screen and (min-width: 1500px) {
  .bannerHeroes {
    font-size: small;
    max-width: 450px;
  }
}
</style>
