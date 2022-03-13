<template>
  <div>
    <h2 v-if="!admin">{{banner.title}}</h2>
    <div v-if="admin">
      <button @click="$emit('move-left')">&#129044;</button>
      <input v-model="banner.title"/>
      <button @click="$emit('remove-banner')">DELETE BANNER</button>
      <button @click="$emit('move-right')">&#10142;</button>
    </div>
    <div v-bind:class="remix ? 'remixHeroes' : 'bannerHeroes'">
      <BannerSlot v-bind:key="`${i}-${hero}`" v-for="(hero, i) in banner.heroes" v-bind:hero="heroes[hero]" v-bind:remix="remix"
      :admin="admin" @change-hero="$emit('change-hero', {slot: i})" />
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
    heroes: {},
    remix: Boolean,
    admin: Boolean
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
.remixHeroes {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  margin:auto;
  font-size: x-small;
  max-width: 266px;
}
@media only screen and (min-width: 400px) {
  .bannerHeroes {
    font-size: small;
  }
  .remixHeroes {
    font-size: small;
  }
}
@media only screen and (min-width: 1500px) {
  .bannerHeroes {
    font-size: small;
    max-width: 450px;
  }
  .remixHeroes {
    font-size: small;
    max-width: 300px;
  }
}
</style>
