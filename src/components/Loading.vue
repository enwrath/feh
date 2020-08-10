<template>
  <div v-if="visible" class="loader">
  </div>
</template>

<script>
export default {
  name: 'Loading',
  props: {
    visible: Boolean
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.loader {
  margin: auto;
  border: 0.75em solid #5f5d5d;
  border-right: 0.75em solid #68f784;
  border-radius: 50%;
  width: 3em;
  height: 3em;
  animation: spin 1.5s ease-in-out infinite;
}
@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(720deg); }
}
</style>
