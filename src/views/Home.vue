<template>
  <div>
    <TextBubble :bubbletext="'You can click the heroes to check their seasons and more! Click again to see their fodder!'" :imagename="'tikihelp'" />
    <h1>Upcoming legendary/mythic banners</h1>
    <div class="bannerList">
      <div v-bind:key="banner.title" v-for="banner in banners.legendary">
        <Banner v-bind:banner="banner" v-bind:heroes="heroes" v-bind:remix="false" />
      </div>
    </div>
    <h1>Upcoming remix legendary banners</h1>
    <div class="bannerList">
      <div v-bind:key="`remix-${banner.title}`" v-for="banner in banners.remix">
        <Banner v-bind:banner="banner" v-bind:heroes="heroes"  v-bind:remix="true" />
      </div>
    </div>
  </div>
</template>

<script>

// @ is an alias to /src
import Banner from '@/components/Banner.vue'
import TextBubble from '@/components/TextBubble.vue'
import bannerjson from "@/assets/banners.json";
import herojson from "@/assets/heroes.json";

export default {
  name: 'Home',
  components: {
    Banner, TextBubble
  },
  data() {
    return {
      heroes: herojson,
      banners: bannerjson
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bannerList {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
.bannerList > div {
  margin: auto;
  background-color: #150101;
  padding: 0.25rem;
  margin-bottom: 1rem;
}
</style>
