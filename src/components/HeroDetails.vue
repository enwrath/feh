<template>
  <div>
    <p>
      {{ hero.name }} - {{ hero.season }}
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
div {
  background-color: white;
}
</style>
