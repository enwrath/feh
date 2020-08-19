<template>
  <div class="mainDiv">
    <div>
      <p><a :href="hero.gamepedia">{{ hero.name }}</a></p>
      <p>{{ hero.season }} | {{ hero.bst }} BST</p>
      <p>Boost: {{ hero.boost }}</p>
      <p>{{ hero.effect }}</p>
    </div>
    <div class="heroSkills">
      <p>Inheritable skills:</p>
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
    hero: {}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.mainDiv {
  display: flex;
  flex-wrap: wrap;
  background-color: #dedede;
  border-style: solid;
  border-width: thin;
  box-sizing: border-box;
  border-radius: 1em;
}
.mainDiv > div {
  padding: 10px;
  box-sizing: border-box;
}
.mainDiv > :first-child {
  border-right-style: solid;
  border-width: thin;
}
p:first-of-type {
  text-align: center;
  font-weight: bold;
}
</style>
