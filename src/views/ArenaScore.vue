<template>
  <div>
    <div class="units">
      <ArenaUnit @unitscore="unitscore1 = $event" />
      <ArenaUnit @unitscore="unitscore2 = $event" />
      <ArenaUnit @unitscore="unitscore3 = $event" />
      <ArenaUnit @unitscore="unitscore4 = $event" />
    </div>

    <p class="scores">
      Score: {{ minScore + 2 }} ({{ totalScore }}) | Range: {{ minScore }} - {{ minScore + 14 }}
    </p>
    <p>
      Units are assumed to be 5* and level 40. Score in parenthesis is unrounded score.
    </p>
    <p>
      Score formula from a
      <a href="https://www.reddit.com/r/OrderOfHeroes/comments/7ritua/from_the_makers_of_the_most_accurate_arena_score/">
        Reddit post</a>
      by patoente.
    </p>
    <p>
      More user friendly calculator by <a href="http://www.arcticsilverfox.com/score_calc/">arcticsilverfox</a>.
    </p>
  </div>
</template>

<script>
import ArenaUnit from '@/components/ArenaUnit.vue'

export default {
  name: 'ArenaScore',
  components: {
    ArenaUnit
  },
  data() {
    return {
      unitscore1: 0,
      unitscore2: 0,
      unitscore3: 0,
      unitscore4: 0,
    }
  },
  computed: {
    totalScore: function () {
      return (150 + (this.unitscore1 + this.unitscore2 + this.unitscore3 + this.unitscore4) / 4 ) * 2;
    },
    minScore: function() {
      return Math.floor(this.totalScore) % 2 === 0 ? Math.floor(this.totalScore) - 2 : Math.floor(this.totalScore) - 3;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.scores {
  font-weight: bolder;
}
.units {
  display: flex;
  flex-wrap: wrap;
  max-width: 800px;
  margin: auto;
}
</style>
