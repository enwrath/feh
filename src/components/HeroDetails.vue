<template>
  <div class="mainDiv">
    <div>
      <img v-bind:src="`./images/${hero.name}.webp`" v-bind:class="hero.color" />
      <br />
      <p>{{ hero.name }} - {{ hero.season }}</p>
      <p>Blessing: xHP yStat</p>
    </div>
    <div class="heroSkills">
      <p>
        Life and death XIV: Terror from deep
      </p>
      <p>
        B Skill
      </p>
    </div>
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
  display: flex;
  flex-direction: row;
}
.mainDiv > div {
  flex-basis: 50%;
}
div {
  background-color: white;
  border-style: solid;
  border-width: thin;
  box-sizing: border-box;
  text-align: center;
}
img {
  max-width: 100%;
  height: auto;
  border-style: solid;
  border-width: thick;
  box-sizing: border-box;
}
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
</style>
