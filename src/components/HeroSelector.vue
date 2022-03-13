<template>
  <div>
    <button @click="$emit('select-cancel')">CANCEL AND RETURN</button>
    {{ currHero }}
    <button @click="$emit('select-confirm', currHero)">SAVE AND RETURN</button>
    <hr />
    <img @click="currHero=hero.name" v-bind:key="`img-${i}-${hero}`" v-for="(hero, i) in heroes" :src="`./images/${hero.name}.webp`" :class="hero.color" />
  </div>
</template>

<script>
export default {
  name: 'HeroSelector',
  props: {
    heroes: {},
    oldHero: String
  },
  data() {
    return {
      currHero: this.oldHero
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
img {
  max-width: 100%;
}
</style>
