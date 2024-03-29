<template>
  <div>
    <div v-if="!loadComplete">
      Loading...
    </div>
    <div v-if="loadComplete">
      <h1>ADMIN MODE ON</h1>
      <button @click="exportBannerJSON">Copy banners JSON</button>
      <button @click="exportHeroesJSON">Copy heroes JSON</button>
      <HeroSelector v-if="selectHero" :heroes="heroes" :oldHero="heroChange.name"
      @select-confirm="changeSlot"
      @add-hero="addHero" @del-hero="delHero"></HeroSelector>
      <div v-else>

        <h1>Upcoming legendary/mythic banners</h1>
        <TextBubble :bubbletext="note" v-bind:key="`note-legendary-${i}`" v-for="(note, i) in banners.notes.legendary" :imagename="'faehelp'" />
        <div class="bannerList">
          <div v-bind:key="`legendary-${i}`" v-for="(banner, i) in banners.legendary">
            <Banner v-bind:banner="banner" v-bind:heroes="heroes" :admin="true" @remove-banner="removeBanner(i, false)"
            @move-left="moveBanner(i, false, false)" @move-right="moveBanner(i, true, false)" @change-hero="changeHero(i, false, ...arguments)"
            @del-col="deleteCol(i, false)" @add-col="addCol(i, false)" />
          </div>
          <div>
            <button @click="newBanner(false)">Add new banner</button>
          </div>
        </div>
        <h1>Upcoming remix legendary banners</h1>
        <TextBubble :bubbletext="note" v-bind:key="`note-remix-${i}`" v-for="(note, i) in banners.notes.remix" :imagename="'faehelp'" />
        <div class="bannerList">
          <div v-bind:key="`remix-${i}`" v-for="(banner, i) in banners.remix">
            <Banner v-bind:banner="banner" v-bind:heroes="heroes" :admin="true" @remove-banner="removeBanner(i, true)"
            @move-left="moveBanner(i, false, true)" @move-right="moveBanner(i, true, true)" @change-hero="changeHero(i, true, ...arguments)"
            @del-col="deleteCol(i, true)" @add-col="addCol(i, true)" />
          </div>
          <div>
            <button @click="newBanner(true)">Add new banner</button>
          </div>
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
import defaultsjson from "@/assets/defaults.json";

export default {
  name: 'AdminView',
  components: {
    Banner, TextBubble, HeroSelector
  },
  data() {
    return {
      heroes: {},
      banners: {},
      defaults: defaultsjson,
      selectHero: false,
      heroChange: {name: "RED", index: 0, slot: 0, remix: false}
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
  },
  methods: {
    exportBannerJSON: function() {
      let result = JSON.stringify(this.banners);
      navigator.clipboard.writeText(result).then(function() {
        console.log("copied data to clipboard");
      }, function() {
        console.log("couldn't copy to clipboard, pasting to console:");
        console.log(result);
      });
    },
    exportHeroesJSON: function() {
      let result = JSON.stringify(this.heroes);
      navigator.clipboard.writeText(result).then(function() {
        console.log("copied data to clipboard");
      }, function() {
        console.log("couldn't copy to clipboard, pasting to console:");
        console.log(result);
      });
    },
    delHero: function(e) {
      if (e in this.heroes) {
        delete this.heroes[e];
      }
    },
    addHero: function(e) {
      if (!(e in this.heroes)) {
        let h = JSON.parse(JSON.stringify(this.defaults.hero));
        h.name = e;
        this.heroes[e] = h;
      }
    },
    heroSkillsFix: function() {
      //After editing skills won't be in array anymore, fix it
      for (const i of Object.keys(this.heroes)) {
        const hero = this.heroes[i];
        if (!("skills" in hero)) continue;
        if (!Array.isArray(hero.skills)) {
          hero.skills = hero.skills.split(",");
        }
      }
    },
    changeSlot: function(e) {
      if (this.heroChange.remix) {
        this.banners.remix[this.heroChange.index].heroes[this.heroChange.slot] = e;
      } else {
        this.banners.legendary[this.heroChange.index].heroes[this.heroChange.slot] = e;
      }
      this.selectHero = false;
      this.heroSkillsFix();
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
    },
    addCol: function(index, remix) {
      if (!remix) {
        let cols = Math.ceil(this.banners.legendary[index].heroes.length / 4);
        this.banners.legendary[index].heroes.splice(4*cols, 0, "COLORLESS");
        this.banners.legendary[index].heroes.splice(3*cols, 0, "GREEN");
        this.banners.legendary[index].heroes.splice(2*cols, 0, "BLUE");
        this.banners.legendary[index].heroes.splice(cols, 0, "RED");
      } else {
        let cols = Math.ceil(this.banners.remix[index].heroes.length / 4);
        this.banners.remix[index].heroes.splice(4*cols, 0, "COLORLESS");
        this.banners.remix[index].heroes.splice(3*cols, 0, "GREEN");
        this.banners.remix[index].heroes.splice(2*cols, 0, "BLUE");
        this.banners.remix[index].heroes.splice(cols, 0, "RED");
      }
    },
    deleteCol: function(index, remix) {
      if (!remix) {
        let cols = Math.ceil(this.banners.legendary[index].heroes.length / 4);
        this.banners.legendary[index].heroes.splice(4*cols-1, 1);
        this.banners.legendary[index].heroes.splice(3*cols-1, 1);
        this.banners.legendary[index].heroes.splice(2*cols-1, 1);
        this.banners.legendary[index].heroes.splice(cols-1, 1);
      } else {
        let cols = Math.ceil(this.banners.remix[index].heroes.length / 4);
        this.banners.remix[index].heroes.splice(4*cols-1, 1);
        this.banners.remix[index].heroes.splice(3*cols-1, 1);
        this.banners.remix[index].heroes.splice(2*cols-1, 1);
        this.banners.remix[index].heroes.splice(cols-1, 1);
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
