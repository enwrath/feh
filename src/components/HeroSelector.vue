<template>
  <div>
    <button @click="$emit('select-confirm', currHero)">Select this hero</button>
    <br />
    <img :src="`${baseUrl}${currHero}.webp`" :class="heroes[currHero].color" />
    <span>Name: </span><input v-model="heroes[currHero].name" disabled />
    <span>Color: </span>
    <select v-model="heroes[currHero].color">
      <option value="Red">Red</option>
      <option value="Blue">Blue</option>
      <option value="Green">Green</option>
      <option value="Colorless">Colorless</option>
    </select>
    <span>Season: </span>
    <select v-model="heroes[currHero].season">
      <option value="Earth">Earth</option>
      <option value="Fire">Fire</option>
      <option value="Water">Water</option>
      <option value="Wind">Wind</option>
      <option value="Light">Light</option>
      <option value="Dark">Dark</option>
      <option value="Astra">Astra</option>
      <option value="Anima">Anima</option>
    </select>
    <span>BST: </span><input v-model="heroes[currHero].bst" type="number" /> <br />
    <span>Boost: </span><input v-model="heroes[currHero].boost"  />
    <span>Effect: </span><input v-model="heroes[currHero].effect"  />
    <span>Wikilink: </span><input v-model="heroes[currHero].gamepedia"  /> <br />
    <span>Skills: (separate with ,) </span><input v-model="heroes[currHero].skills"  />

    <button @click="deleteHero">DELETE HERO</button>
    <hr />
    <div>
      <span>Name</span><input v-model="newHero" />
      <button @click="addHero">Add new hero</button>
    </div>
    <img @click="currHero=hero.name" v-bind:key="`img-${i}-${hero}`" v-for="(hero, i) in heroes" :src="`./images/${hero.name}.webp`" :class="hero.color" />
  </div>
</template>

<script>
export default {
  name: 'HeroSelector',
  props: {
    heroes: {},
    oldHero: String
  },
  data() {
    return {
      currHero: this.oldHero,
      newHero: "NewHero",
      baseUrl: "https://resilient-belekoy-cf9d2e.netlify.app/feh/images/"
    }
  },
  methods: {
    addHero: function() {
      this.$emit("add-hero", this.newHero);
      this.currHero = this.newHero;
    },
    deleteHero: function() {
      this.$emit("del-hero", this.currHero);
      this.currHero = "RED";
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.Red {
  background-color: #f78484;
}
.Blue {
  background-color: #afd5ff;
}
.Green {
  background-color: #94f194;
}
.Colorless {
  background-color: #c3c3c3;
}
img {
  max-width: 100%;
}
</style>
