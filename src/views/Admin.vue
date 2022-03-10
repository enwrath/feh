<template>
  <div>
    <h1>ADMIN MODE ON</h1>
    <h1>Upcoming legendary/mythic banners</h1>
    <TextBubble :bubbletext="note" v-bind:key="`note-legendary-${i}`" v-for="(note, i) in banners.notes.legendary" :imagename="'faehelp'" />
    <div class="bannerList">
      <div v-bind:key="`legendary-${i}`" v-for="(banner, i) in banners.legendary">
        <Banner v-bind:banner="banner" v-bind:heroes="heroes" v-bind:remix="false" :admin="true" />
      </div>
      <div>
        <button @click="newBanner(false)">Add new banner</button>
      </div>
    </div>
    <h1>Upcoming remix legendary banners</h1>
    <TextBubble :bubbletext="note" v-bind:key="`note-remix-${i}`" v-for="(note, i) in banners.notes.remix" :imagename="'faehelp'" />
    <div class="bannerList">
      <div v-bind:key="`remix-${banner.title}`" v-for="banner in banners.remix">
        <Banner v-bind:banner="banner" v-bind:heroes="heroes"  v-bind:remix="true" :admin="true" />
      </div>
    </div>
  </div>
</template>

<script>

// @ is an alias to /src
import Banner from '@/components/Banner.vue';
import TextBubble from '@/components/TextBubble.vue';
import bannerjson from "@/assets/banners.json";
import herojson from "@/assets/heroes.json";
import defaultsjson from "@/assets/defaults.json";

export default {
  name: 'AdminView',
  components: {
    Banner, TextBubble
  },
  data() {
    return {
      heroes: herojson,
      banners: bannerjson,
      defaults: defaultsjson
    }
  },
  methods: {
    newBanner: function(remix) {
      if (!remix) {
        this.banners.legendary.push(JSON.parse(JSON.stringify(this.defaults.legendary)))
      }
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
