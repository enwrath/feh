<template>
  <div>
    <h1>Upcoming legendary/mythic banners</h1>
    <div v-bind:key="banner.title" v-for="banner in banners">
      <Banner v-bind:banner="banner" />
    </div>
  </div>
</template>

<script>

// @ is an alias to /src
import Banner from '@/components/Banner.vue'

export default {
  name: 'Calendar',
  components: {
    Banner
  },
  data() {
    return {
      heroes: {
        "???": {
          name: "???"
        },
        "Fjorm": {
          name: "Fjorm",
          season: "Water"
        },
        "Gunnthra": {
          name: "Gunnthra",
          season: "Wind"
        }
      },
      banners: [
        {
          title: "August 2020",
          heroes: ["Fjorm", "???"]
        },
        {
          title: "September 2020",
          heroes: ["Fjorm", "Gunnthra"]
        }
      ]
    }
  },
  created() {
    this.banners.forEach(obj => {
      for (const prop in obj) {
          if (prop === 'heroes') {
            obj[prop] = obj[prop].map(h => this.heroes[h]);
            console.log(obj[prop]);
          }
      }
    });
  }
}
</script>
