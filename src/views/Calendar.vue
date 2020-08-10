<template>
  <div>
    <h1>Upcoming legendary/mythic banners</h1>
    <div v-bind:key="banner.title" v-for="banner in banners">
      <Banner v-bind:banner="banner" v-bind:heroes="heroes" />
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
  }
}
</script>
