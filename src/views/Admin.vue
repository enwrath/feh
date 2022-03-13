<template>
  <div>
    <h1>ADMIN MODE ON</h1>
    <HeroSelector v-if="selectHero" :heroes="heroes" :oldHero="heroChange.name"
    @select-cancel="selectHero=false" @select-confirm="changeSlot"></HeroSelector>
    <div v-else>

      <h1>Upcoming legendary/mythic banners</h1>
      <TextBubble :bubbletext="note" v-bind:key="`note-legendary-${i}`" v-for="(note, i) in banners.notes.legendary" :imagename="'faehelp'" />
      <div class="bannerList">
        <div v-bind:key="`legendary-${i}`" v-for="(banner, i) in banners.legendary">
          <Banner v-bind:banner="banner" v-bind:heroes="heroes" v-bind:remix="false" :admin="true" @remove-banner="removeBanner(i, false)"
          @move-left="moveBanner(i, false, false)" @move-right="moveBanner(i, true, false)" @change-hero="changeHero(i, false, ...arguments)"/>
        </div>
        <div>
          <button @click="newBanner(false)">Add new banner</button>
        </div>
      </div>
      <h1>Upcoming remix legendary banners</h1>
      <TextBubble :bubbletext="note" v-bind:key="`note-remix-${i}`" v-for="(note, i) in banners.notes.remix" :imagename="'faehelp'" />
      <div class="bannerList">
        <div v-bind:key="`remix-${i}`" v-for="(banner, i) in banners.remix">
          <Banner v-bind:banner="banner" v-bind:heroes="heroes"  v-bind:remix="true" :admin="true" @remove-banner="removeBanner(i, true)"
          @move-left="moveBanner(i, false, true)" @move-right="moveBanner(i, true, true)" />
        </div>
        <div>
          <button @click="newBanner(true)">Add new banner</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

// @ is an alias to /src
import Banner from '@/components/Banner.vue';
import HeroSelector from '@/components/HeroSelector.vue';
import TextBubble from '@/components/TextBubble.vue';
import bannerjson from "@/assets/banners.json";
import herojson from "@/assets/heroes.json";
import defaultsjson from "@/assets/defaults.json";

export default {
  name: 'AdminView',
  components: {
    Banner, TextBubble, HeroSelector
  },
  data() {
    return {
      heroes: herojson,
      banners: bannerjson,
      defaults: defaultsjson,
      selectHero: false,
      heroChange: {name: "RED", index: 0, slot: 0, remix: false}
    }
  },
  methods: {
    changeSlot: function(e) {
      if (this.heroChange.remix) {
        this.banners.remix[this.heroChange.index].heroes[this.heroChange.slot] = e;
      } else {
        this.banners.legendary[this.heroChange.index].heroes[this.heroChange.slot] = e;
      }
      this.selectHero = false;
    },
    changeHero: function(index, remix, e) {
      this.heroChange.slot = e.slot;
      this.selectHero = true;
      this.heroChange.name = remix ? this.banners.remix[index].heroes[e.slot] : this.banners.legendary[index].heroes[e.slot];
      this.heroChange.index = index;
      this.heroChange.remix = remix;
    },
    newBanner: function(remix) {
      if (!remix) {
        this.banners.legendary.push(JSON.parse(JSON.stringify(this.defaults.legendary)));
      } else {
        this.banners.remix.push(JSON.parse(JSON.stringify(this.defaults.remix)));
      }
    },
    removeBanner: function(index, remix) {
      if (!remix) {
        this.banners.legendary.splice(index, 1);
      } else {
        this.banners.remix.splice(index, 1);
      }
    },
    moveBanner: function(index, right, remix) {
      let newIndex = right ? index + 1 : index - 1;
      if (newIndex < 0 || (!remix && newIndex >= this.banners.legendary.length) || (remix && newIndex >= this.banners.remix.length)) {
        return;
      }
      if (!remix) {
        let old = this.banners.legendary[newIndex];
        this.banners.legendary.splice(newIndex, 1, this.banners.legendary[index])
        this.banners.legendary.splice(index, 1, old)
      } else {
        let old = this.banners.remix[newIndex];
        this.banners.remix.splice(newIndex, 1, this.banners.remix[index])
        this.banners.remix.splice(index, 1, old)
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
