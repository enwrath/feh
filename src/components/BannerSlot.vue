<template>
  <div>
    {{hero.name}} * {{hero.season}}

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
</style>
