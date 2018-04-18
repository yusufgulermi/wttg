<template>
  <div class="content">
    <h1>Welcome to the Game II key organizer</h1>
    <b-field>
      <b-input v-model="fullKey" type="textarea" readonly/>
    </b-field>
    <div class="columns">
      <div class="column">
        <p :class="{ 'has-text-danger': wiki1, 'has-text-weight-bold': wiki1 }">Wiki 1 keys: {{ wikiKeys["1"] }}</p>
      </div>
      <div class="column">
        <p :class="{ 'has-text-danger': wiki2, 'has-text-weight-bold': wiki2 }">Wiki 2 keys: {{ wikiKeys["2"] }}</p>
      </div>
      <div class="column">
        <p :class="{ 'has-text-danger': wiki3, 'has-text-weight-bold': wiki3 }">Wiki 3 keys: {{ wikiKeys["3"] }}</p>
      </div>
    </div>
    <section>
      <inputf :keynum="1" v-model="keyw[0]"/>
      <inputf :keynum="2" v-model="keyw[1]"/>
      <inputf :keynum="3" v-model="keyw[2]"/>
      <inputf :keynum="4" v-model="keyw[3]"/>
      <inputf :keynum="5" v-model="keyw[4]"/>
      <inputf :keynum="6" v-model="keyw[5]"/>
      <inputf :keynum="7" v-model="keyw[6]"/>
      <inputf :keynum="8" v-model="keyw[7]"/>
    </section>
  </div>
</template>

<script>

import InputField from './InputField.vue'

export default {
  name: 'HelloWorld',
  components: {
    'inputf': InputField
  },
  data () {
    return {
      keyw: this._.fill(Array(8), {key: '', wiki: 0}),
      msg: 'Welcome to Your Vue.js App'
    }
  },
  computed: {
    wiki1: function () {
      return (this.wikiKeys['1'] > 3)
    },
    wiki2: function () {
      return (this.wikiKeys['2'] > 3)
    },
    wiki3: function () {
      return (this.wikiKeys['3'] > 3)
    },
    wikiKeys: function () {
      var d = this.wikiCount
      if (!('1' in d)) {
        d['1'] = 0
      }
      if (!('2' in d)) {
        d['2'] = 0
      }
      if (!('3' in d)) {
        d['3'] = 0
      }
      return d
    },
    wikiCount: function () {
      return this._.countBy(this.keyw, this._.iteratee('wiki'))
    },
    fullKey: function () {
      if (this._.every(this.keyw, function (a) { return a.key.length === 12 })) {
        // return 'asd'
        var final = ''
        this._.forEach(this.keyw, function (value) {
          final = final + value.key
        })
        return final
      } else {
        return ''
      }
    }
  },
  methods: {
    tester: function (value) {
      this.test = value
    }
  }
}
</script>

<style>
</style>
