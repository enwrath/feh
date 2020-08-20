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
  max-width: 480px;

}
.bannerHeroes > div {
  width: 33%;
  height: 25%;
}
</style>
