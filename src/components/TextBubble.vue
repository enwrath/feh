<template>
  <div class="main">
    <img :src="`./images/${imagename}.webp`" />
    <div class="bubble">
      <span>{{ bubbletext }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TextBubble',
  props: {
    bubbletext: String,
    imagename: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.main {
  display: flex;
  flex-direction: row;
  margin-top: 1em;
}
.bubble {
  position: relative;
	background: #150101;
	border-radius: .4em;
  display: inline-block;
  display: flex;
  align-items: center;
  margin: 0.5em 0 0.5em 1em;
  padding: 1em;
}

.bubble:after {
	content: '';
	position: absolute;
	left: 0;
	top: 50%;
	width: 0;
	height: 0;
	border: 1em solid transparent;
	border-right-color: #150101;
	border-left: 0;
	margin-top: -1em;
	margin-left: -1em;
}
img {
  max-height: 5em;
}
</style>
