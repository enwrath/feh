<template>
  <div v-bind:class="['bannerHero', hero.color]" v-on:click="nextPage" :style="cssProps">
    <div class="imgDiv">


      <img :style="{visibility: currPage === 0 || !('season' in hero) ? 'visible' : 'hidden'}" v-bind:src="`${baseUrl}${hero.name}.webp`" />

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
    hero: {},
    admin: Boolean,
    size: Number
  },
  data() {
    return {
      currPage: 0,
      baseUrl: "https://resilient-belekoy-cf9d2e.netlify.app/feh/images/"
    }
  },
  methods: {
    nextPage: function() {
      if (this.admin) this.$emit('change-hero')
      else {
        this.currPage += 1;
        this.currPage %= 3;
      }
    }
  },
  computed: {
    cssProps() {
      return {
        '--unit-width': (Math.round((100/this.size) * 100) / 100).toString()+"%"
      }
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
  background-color: #c3c3c3;
}
.bannerHero {
  display: inline-block;
  position: relative;
  width: var(--unit-width);
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
