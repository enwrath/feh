<template>
  <div class="bannerHero" v-bind:class="hero.color" >
    <img v-bind:src="`./images/${hero.name}.webp`"/>
  </div>
</template>

<script>
export default {
  name: 'BannerSlot',
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
}
</style>
