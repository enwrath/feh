<template>
  <div class="mainDiv">
    <p><a v-on:click.stop="" :href="hero.gamepedia" target="_blank">{{ hero.name }}</a></p>
    <hr />
    <p>{{ hero.season }} | {{ hero.bst }} BST</p>
    <p>Boost: {{ hero.boost }}</p>
    <p>{{ hero.effect }}</p>
    <hr />
    <p v-for="skill in hero.skills" :key="skill">
      {{ skill }}
    </p>
  </div>
</template>

<script>
export default {
  name: 'HeroDetails',
  props: {
    hero: {}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.mainDiv {
  background-color: #ffffff69;
  border-style: solid;
  border-width: thick;
  box-sizing: border-box;
}
</style>
