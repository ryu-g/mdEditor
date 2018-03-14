<template lang='pug'>
  div#app
    div.textArea
      textarea(v-model='input')

    div.previewArea(v-html= 'output')
</template>


<script>
import marked from'marked'
import highlight from'highlight.js'
import 'highlight.js/styles/monokai.css'
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
    highlight.initHighlightingOnLoad()
    this.output= marked(this.input)
  }
}

marked.setOptions({
    highlight: function(code, lang) {
        return highlight.highlightAuto(code, [lang]).value
    }
})
</script>


<style lang="sass">
html, body
  height: 100%
  margin: 0

textarea 
  font-family: courier, monospace
  font-size: 12px
  background-color: #56040c
  width: 100%
  height: 100%
  color: #EDEDED
  overflow-y: scroll 
  padding: 9px

h1
  font-size: 18px

h2,h3
  font-size: 16px
  margin-top: 20px 
  margin-bottom: 5px 

p,li,td,tr
  font-size: 14px

  margin: 0

table
  display: table
  width: calc(100% - 10px)
  marign: 10px 0
  background-color: #EEE
  // margin: 0 auto

pre>code
  font-family: courier, monospace
  // font-weight: 100

pre
  padding: 15px
  background-color: #333
  color: #EEE
  margin-right: 10px

p>code
  font-family: courier, monospace
  padding: 5px
  background-color: #EEE
  color: #333

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
  font-weight: 100
  padding-left: 10px
  width: 50%
  min-height: 100%
  color: #2c3e50
  overflow-y: scroll 

.center
  text-align: center

@media print
  .textArea
    display: none

  .previewArea
    width: 100% 
    overflow-y: visible

</style>
