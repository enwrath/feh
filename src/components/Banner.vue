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
  justify-content: center;
}
.bannerHeroes > div {
  width: 158px;
  flex-basis: 15%;
}
@media only screen and (max-width: 1000px) {
  .bannerHeroes > div {
    flex-basis: 30%;
  }
}
</style>
