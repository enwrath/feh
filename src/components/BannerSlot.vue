<template>
  <div class="bannerHero" v-bind:class="hero.color" >
    <div>
      <img src="https://i.imgur.com/a1Wyr2m.png">
    </div>
    {{hero.name}}
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
  border-radius: 1rem;
  margin: 0.5rem;
}
img {
  max-width: 100%;
  height: auto;
}
</style>
