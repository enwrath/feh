<template>
  <div class="mainDiv">
    <div v-if="currPage === 1">
      <p><a v-on:click.stop="" :href="hero.gamepedia" target="_blank">{{ hero.name }}</a></p>
      <p>{{ hero.season }} | {{ hero.bst }} BST</p>
      <p>Boost: {{ hero.boost }}</p>
      <p>{{ hero.effect }}</p>
    </div>
    <div v-if="currPage === 2">
      <p class="title">
        Noteworthy fodder:
      </p>
      <p v-for="skill in hero.skills" :key="skill">
        {{ skill }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HeroDetails',
  props: {
    hero: {},
    currPage: Number
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
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
}
.title {
  text-decoration: underline;
}
</style>
