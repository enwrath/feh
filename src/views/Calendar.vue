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
import bannerjson from "@/assets/banners.json";
import herojson from "@/assets/heroes.json";

export default {
  name: 'Calendar',
  components: {
    Banner
  },
  data() {
    return {
      heroes: herojson,
      banners: bannerjson
    }
  }
}
</script>
