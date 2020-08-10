<template>
  <div>
    {{banner.title}}
    <div v-bind:key="hero" v-for="hero in banner.heroes">
      <BannerSlot v-bind:hero="heroes[hero]" />
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
</style>
