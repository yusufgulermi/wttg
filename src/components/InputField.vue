<template>
  <b-field
    :label="keyname"
    :type="error"
    :message="errormsg"
    horizontal>
    <b-field :type="error">
      <b-input v-model="inputText" :placeholder="keyname" expanded/>
      <div class="control">
        <b-radio-button v-model="radioButton" native-value="1">
          1
        </b-radio-button>
      </div>
      <div class="control">
        <b-radio-button v-model="radioButton" native-value="2">
          2
        </b-radio-button>
      </div>
      <div class="control">
        <b-radio-button v-model="radioButton" native-value="3">
          3
        </b-radio-button>
      </div>
    </b-field>
  </b-field>
</template>

<script>
export default {
  props: {
    'keynum': {
      type: Number,
      default: 0
    }
  },
  data () {
    return {
      keyw: {
        key: '',
        wiki: 0
      },
      key: '',
      radioButton: '',
      inputText: '',
      errormsg: 'Awaiting input.',
      isError: null
    }
  },
  computed: {
    keyname: function () {
      return 'Key ' + this.keynum
    },
    error: function () {
      if (this.isError === null) {
        return ''
      } else if (this.isError) {
        return 'is-danger'
      } else {
        return 'is-success'
      }
    }
  },
  watch: {
    radioButton: function () {
      this.keyw.wiki = Number(this.radioButton)
      this.$emit('input', this.keyw)
    },
    inputText: function () {
      if (this.inputText === '') {
        this.key = ''
        this.isError = null
        this.errormsg = 'Awaiting input.'
        return
      }
      var re = /(?:\s|^)([\da-f]{12})(?![\w\d])/g
      var results = this.inputText.match(re)
      if (results === null) { // no results
        this.key = ''
        this.isError = true
        var re2 = /(?:\s|^)([\da-f]{9,11})(?![\w\d])/g
        var results2 = this.inputText.match(re2)
        if (results2 === null) { // no results
          this.errormsg = 'No keys found in text.'
        } else if (results2.length === 1) {
          var len = 12 - results2[0].trim().length
          this.errormsg = 'Missing ' + len + ' character(s) in Key.'
        } else { // >1 result
          console.log(results2)
          var len2 = 12 - results2.sort(function (a, b) { return b.trim().length - a.trim().length })[0].trim().length
          this.errormsg = 'Missing at least ' + len2 + ' character(s) in Key.'
        }
      } else if (results.length === 1) {
        this.key = results[0].trim()
        this.isError = false
        this.errormsg = results[0].trim()
      } else { // >1 result
        this.key = ''
        this.isError = true
        this.errormsg = 'More than 1 key found in text.'
      }
      this.keyw.key = this.key
      this.$emit('input', this.keyw)
    }
  }
}
</script>

<style>
@media screen and (min-width: 769px) {
  .field-label {
    flex-basis: auto;
    flex-grow: unset;
    flex-shrink: unset;
    margin-right: 1.5rem;
    text-align: left;
  }
}
</style>
