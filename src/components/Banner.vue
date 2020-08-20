<template>
  <div>
    <h2>{{banner.title}}</h2>
    <div class="bannerHeroes">
      <BannerSlot v-bind:key="`R1${i}-${hero}`" v-for="(hero, i) in banner.heroes.filter((x,i) => [0,3,6,9].includes(i))" v-bind:hero="heroes[hero]" />
      <BannerSlot v-bind:key="`R2${i}-${hero}`" v-for="(hero, i) in banner.heroes.filter((x,i) => [1,4,7,10].includes(i))" v-bind:hero="heroes[hero]" />
      <BannerSlot v-bind:key="`R3${i}-${hero}`" v-for="(hero, i) in banner.heroes.filter((x,i) => [2,5,8,11].includes(i))" v-bind:hero="heroes[hero]" />
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
  max-width: 640px;

}
.bannerHeroes > div {
  width: 25%;
  height: 33%;
}
</style>
