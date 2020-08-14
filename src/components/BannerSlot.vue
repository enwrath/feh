<template>
  <div class="bannerHero" v-bind:class="hero.color" >
    <div>

      <p>{{hero.name}}</p>
      <img v-bind:src="`./images/${hero.name}.png`"/>
    </div>

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
}
img {
  max-width: 100%;
  height: auto;
  background-color: #ffffff69;
}
p {
  font-weight: bold;
}
</style>
