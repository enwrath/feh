<template>
  <div :style="cssProps">
    <h2 v-if="!admin">{{banner.title}}</h2>
    <div v-if="admin">
      <button @click="$emit('move-left')">&#129044;</button>
      <input v-model="banner.title"/>
      <button @click="$emit('remove-banner')">DELETE BANNER</button>
      <button @click="$emit('move-right')">&#10142;</button>
    </div>
    <div class="bannerHeroes">
      <BannerSlot v-bind:key="`${i}-${hero}`" v-for="(hero, i) in banner.heroes" v-bind:hero="heroes[hero]"
      :admin="admin" :size="perRow" @change-hero="$emit('change-hero', {slot: i})" />
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
    admin: Boolean
  },
  computed: {
    perRow() {
      return Math.ceil(this.banner.heroes.length / 4)
    },
    cssProps() {
      return {
        '--units-per-row': this.perRow
      }
    }
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
  max-width: calc(var(--units-per-row) * 133px);
}
@media only screen and (min-width: 400px) {
  .bannerHeroes {
    font-size: small;
  }
}
@media only screen and (min-width: 1500px) {
  .bannerHeroes {
    font-size: small;
    max-width: calc(var(--units-per-row) * 150px);
  }
}
</style>
