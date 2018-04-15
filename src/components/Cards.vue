<template>
  <div class="cards">
    <h1>cards</h1>
    <h2>add new card</h2>
    <textarea class="front" v-model="front" placeholder="front"></textarea>
    <textarea class="back" v-model="back" placeholder="back"></textarea>
    <button v-on:click="addCard()">add</button>
    <transition name="fade">
      <div v-if="message !== ''" class="message error" v-html="message">
      </div>
    </transition>
    <transition name="fade">
      <div v-if="front !== '' || back !== ''" class="card current">
        <div class="front">{{ front }}</div>
        <div class="back">{{ back }}</div>
      </div>
    </transition>
    <h2>added cards</h2>
    <transition-group name="list">
    <div v-for="card in savedCards" v-bind:key="card.front">
      <div class="card">
        <div class="front">{{ card.front }}</div>
        <div class="back">{{ card.back }}</div>
      </div>
    </div>
  </transition-group>
  </div>
</template>

<script>
export default {
  name: 'Cards',
  data() {
    return {
      front: '',
      back: '',
      savedCards: [],
      message: ''
    }
  },
  methods: {
    addCard: function() {
      if( !this.validation() ) {
        return false
      }

      this.savedCards.unshift( {
        'front': this.front,
        'back': this.back
      })
      this.front = ''
      this.back = ''
    },

    validation: function() {
      this.message = ''

      if( this.front == '') {
        this.message += "front text is needed <br>"
      }
      if( this.back == '') {
        this.message += "back text is needed <br>"
      }

      let is_duplicate = this.savedCards.filter( function( item, index, array ) {
        return item.front == this.front
      }, this)  //filterの第二引数はcallback内でthisとして使うobject
      if( is_duplicate.length != 0 ) {
        this.message += 'duplicate entry: ' + this.front + '<br>'
      }
      console.log(this.message)
      return ( this.message == '' )? true : false
    }
  }
}
</script>

<style scoped>
.card {
  width: 50vw;
  border: 1px solid #222;
  border-radius: 5px;
  border-spacing: 5px;
  margin: 10px 0px;
  display: table;
  table-layout: fixed;
}
.card .front, .card .back {
  display: table-cell;
  margin: 5px ;
  word-wrap: break-word;
  vertical-align: middle;
  white-space: pre-line;
}
.card .front{
  width: 30%;
}

.current {
  border: 1px solid #888;
  color: #888;
  white-space: pre-wrap;
}

.message {
  max-width: 30vw;
  border-radius: 5px;
  border-spacing: 5px;
  margin: 10px 0px;
  padding: 10px;
  border: 2px solid #333;
}
.error{
  border: 2px solid #d44;
  background-color: #fcc;
  color: #400;
}

/* transition */
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active for below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(-30px);
}
</style>