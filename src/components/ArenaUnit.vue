<template>
  <div>
    <form v-on:change="$emit('unitscore', score)">
      <ul>
        <li>
          <label for="merges">Merges:</label>
          <select v-model.number="merges" id="merges">
            <option v-for="n in 11" :value="n-1" :key="`merge-${n}-1`">
              {{n-1}}
            </option>
          </select>
        </li>

        <li>
          <label for="blessings">Blessings:</label>
          <select v-model.number="blessings" id="blessings">
            <option v-for="n in 4" :value="n-1" :key="`blessing-${n}-1`">
              {{n-1}}
            </option>
          </select>
        </li>

        <li>
          <label for="bst">BST:</label>
          <select v-model.number="bst" id="bst">
            <option v-for="n in [250,245,240,235,230,225,220,215,210,205,200,195,190,185,180,175,170,165,160,155,150,145,140]" :value="n" :key="`bst-${n}`">
              {{n}}
            </option>
          </select>
        </li>

        <li>
          <label for="spWpn">Weapon SP:</label>
          <select v-model.number="spWpn" id="spWpn">
            <option v-for="n in [400,350,300]" :value="n" :key="`wpn-${n}`">
              {{n}}
            </option>
          </select>
        </li>

        <li>
          <label for="spAssist">Assist SP:</label>
          <select v-model.number="spAssist" id="spAssist">
            <option v-for="n in [500,400,300,150]" :value="n" :key="`assist-${n}`">
              {{n}}
            </option>
          </select>
        </li>

        <li>
          <label for="spSpecial">Special SP:</label>
          <select v-model.number="spSpecial" id="spSpecial">
            <option v-for="n in [500,300,200]" :value="n" :key="`special-${n}`">
              {{n}}
            </option>
          </select>
        </li>

        <li>
          <label for="spA">A Skill SP:</label>
          <select v-model.number="spA" id="spA">
            <option v-for="n in [350,300,240,200]" :value="n" :key="`a-${n}`">
              {{n}}
            </option>
          </select>
        </li>

        <li>
          <label for="spB">B Skill SP:</label>
          <select v-model.number="spB" id="spB">
            <option v-for="n in [400,300,240,200]" :value="n" :key="`b-${n}`">
              {{n}}
            </option>
          </select>
        </li>

        <li>
          <label for="spC">C Skill SP:</label>
          <select v-model.number="spC" id="spC">
            <option v-for="n in [300,240,200]" :value="n" :key="`c-${n}`">
              {{n}}
            </option>
          </select>
        </li>

        <li>
          <label for="spSeal">Seal Skill SP:</label>
          <select v-model.number="spSeal" id="spSeal">
            <option v-for="n in [300,240,200,160,100]" :value="n" :key="`seal-${n}`">
              {{n}}
            </option>
          </select>
        </li>
      </ul>

      <li>
        Unit Score: {{ scorevalue }}
      </li>
    </form>
  </div>
</template>

<script>

export default {
  name: 'ArenaUnit',
  data() {
    return {
      merges: 0,
      blessings: 0,
      bst: 170,
      spWpn: 400,
      spAssist: 300,
      spSpecial: 500,
      spA: 300,
      spB: 240,
      spC: 240,
      spSeal: 240
    }
  },
  computed: {
    score: function () {
      return 55 + Math.floor(40 * 7 / 3) + this.merges * 2 + Math.floor(this.spTotal / 100) +
        Math.floor(this.bst / 5) + 4 * this.blessings;
    },
    scorevalue: function () {
      return (this.score + 150) * 2;
    },
    spTotal: function() {
      return this.spWpn + this.spAssist + this.spSpecial + this.spA + this.spB +
      this.spC + this.spSeal;
    }
  },
  created: function () {
    this.$emit('unitscore', this.score)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
  background-color: #150101;
  margin: auto;
  margin-top: 1rem;
}
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1rem;
}
ul {
  padding: 0;
}
li {
  list-style: none;
  margin-bottom: 0.5em;
}
label {
  display: block;
}
select {
  width: 5rem;
  background-color: #dfe0d0;
}
</style>
