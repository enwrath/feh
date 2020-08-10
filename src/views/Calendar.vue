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
      heroes: {},
      banners: []
    }
  },
  async created() {
    fetch("https://api.jsonbin.io/b/5f313b621823333f8f20ef64")
      .then(res => res.json())
      .then(data => this.heroes = data);

    fetch("https://api.jsonbin.io/b/5f313b4b1823333f8f20ef5a")
      .then(res => res.json())
      .then(data => this.banners = data);
  }
}
</script>
