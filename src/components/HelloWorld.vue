<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button v-on:click="init()">reset</button>
  </div>
</template>

<script>
const hello = 'Hello, World.'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: '',
      index: 0,
      wait: 0
    }
  },
  created: function() {
    setInterval(this.addLetter, 100)
  },
  methods: {
    addLetter: function() {
      if( this.wait <= 10 ) {
        if( this.index < hello.length ) {
          this.msg += hello[this.index]
          this.index += 1
        } else {
          this.wait += 1
        }
      } else {
        this.init()
      }
    },
    init: function() {
      this.index = 0
      this.wait = 0
      this.msg = ''
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
  height: 30px;
}
a {
  color: #42b983;
}
</style>
