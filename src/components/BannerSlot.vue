<template>
  <div class="bannerHero" v-bind:class="hero.color" v-on:click="nextPage" >
    <div class="imgDiv">


      <img :style="{visibility: currPage === 0 || !('season' in hero) ? 'visible' : 'hidden'}" v-bind:src="`./images/${hero.name}.webp`" />

      <HeroDetails v-if="currPage !== 0 && 'season' in hero" :hero="hero" :currPage="currPage" />
    </div>
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
      currPage: 0
    }
  },
  methods: {
    nextPage: function() {
      this.currPage += 1;
      this.currPage %= 3;
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
  background-color: #808080;
}
.bannerHero {
  display: inline-block;
  position: relative;
  width: 33.33%;
}
img {
  max-width: 100%;
  display: block;
}
.imgDiv {
  border-style: solid;
  border-color: #150101;
}
</style>
