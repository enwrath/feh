<template>
  <div v-bind:class="hero.color">
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
  background-color: red;
}
.Blue {
  background-color: blue;
}
.Green {
  background-color: green;
}
.Colorless {
  background-color: gray;
}
</style>
