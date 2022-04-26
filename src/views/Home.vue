<template>
  <div>
    <div v-if="!loadComplete">
      Loading...
    </div>
    <div v-if="loadComplete">
      <TextBubble :bubbletext="'You can click the heroes to check their seasons and more! Click again to see their fodder!'" :imagename="'tikihelp'" />
      <h1>Upcoming legendary/mythic banners</h1>
      <TextBubble :bubbletext="note" v-bind:key="`note-legendary-${i}`" v-for="(note, i) in banners.notes.legendary" :imagename="'faehelp'" />
      <div class="bannerList">
        <div v-bind:key="banner.title" v-for="banner in banners.legendary">
          <Banner v-bind:banner="banner" v-bind:heroes="heroes" v-bind:remix="false" :admin="false" />
        </div>
      </div>
      <h1>Upcoming remix legendary banners</h1>
      <TextBubble :bubbletext="note" v-bind:key="`note-remix-${i}`" v-for="(note, i) in banners.notes.remix" :imagename="'faehelp'" />
      <div class="bannerList">
        <div v-bind:key="`remix-${banner.title}`" v-for="banner in banners.remix">
          <Banner v-bind:banner="banner" v-bind:heroes="heroes"  v-bind:remix="true" :admin="false" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>

// @ is an alias to /src
import Banner from '@/components/Banner.vue'
import TextBubble from '@/components/TextBubble.vue'

export default {
  name: 'Home',
  components: {
    Banner, TextBubble
  },
  data() {
    return {
      heroes: {},
      banners: {}
    }
  },
  created: function () {
    fetch("https://resilient-belekoy-cf9d2e.netlify.app/feh/json/heroes.json")
      .then(r => r.json())
      .then(json => {
        this.heroes = json;
    });
    fetch("https://resilient-belekoy-cf9d2e.netlify.app/feh/json/banners.json")
      .then(r => r.json())
      .then(json => {
        this.banners = json;
    });
  },
  computed: {
    loadComplete: function () {
      return Object.keys(this.heroes).length > 0 && Object.keys(this.banners).length > 0;
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
