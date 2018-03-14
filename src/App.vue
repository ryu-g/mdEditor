<template lang='pug'>
  div#app
    div.textArea
      textarea(v-model='input')

    div.previewArea(v-html= 'output')
</template>


<script>
import marked from'marked'

export default {
  name: 'app',
  data () {
    return {
      input: localStorage.getItem('mdEditor_180314'),
      output: ''
    }
  },
  watch: {
    input: function() {
      localStorage.setItem('mdEditor_180314',this.input)
      this.output = marked(this.input)
    }
  },
  mounted(){
    this.output= marked(this.input)
  }
}
</script>


<style lang="sass">
html, body
  height: 100%
  margin: 0

textarea 
  font-family: courier, monospace
  font-size: 16px
  background-color: #56040c
  width: 100%
  height: 100%
  color: #EDEDED
  overflow-y: scroll 
  padding: 9px

h1
  font-size: 22px
  text-align: center

h2,h3
  font-size: 18px
  margin-bottom: 0px

p
  margin: 0

table
  width: 100%
  marign-top: 5px
  background-color: #EEE
  // margin: 0 auto

td
  text-align: center

ul
  margin-top: 0px
  padding-left: 24px

#app 
  font-family: 'Avenir', Helvetica, Arial, sans-serif
  // text-align: 
  color: #2c3e50
  width: 100%
  height: 100%
  display: flex

.textArea
  background-color: #222222
  width: 50%
  height: 100%
  color: #EDEDED
  overflow-y: scroll 

.previewArea
  padding-left: 10px
  width: 50%
  max-height: 100%
  color: #2c3e50
  overflow-y: scroll 

.center
  text-align: center



</style>
