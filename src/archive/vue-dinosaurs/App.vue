<template>
  <div id="card">
    <div>
      <header>{{ title }} <span @click="toggle">{{ editLabel }}</span></header>
      <ul>
        <li v-for="item in items">
          <keep-alive>
            <component v-bind:is="currentView"
            v-bind:name="item.text" v-bind:initialQuantity="item.quantity"
            v-bind:diet="item.diet"></component>
          </keep-alive>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import DinoEdit from './components/DinoEdit'
import DinoShow from './components/DinoShow'

export default {
  components: {
    DinoEdit,
    DinoShow
  },
  data () {
    return {
      title: 'Dinosaurs',
      input: '',
      currentView: 'DinoShow',
      items: [
        { text: 'Tyrannosaurus', quantity: 5, diet: 'Carnivore' },
        { text:'Triceratops', quantity: 4, diet: 'Herbivore' },
        { text: 'Stegosaurus', quantity: 6, diet: 'Herbivore' }
      ]
    }
  },
  methods:{
    toggle: function () {
      this.currentView = this.currentView === 'DinoEdit' ? 'DinoShow' : 'DinoEdit'
    }
  },
  computed:{
    editLabel: function () {
      return this.currentView === 'DinoEdit' ? 'Show' : 'Edit'
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.large {
  width: 100px;
}
.rounded {
  border-radius: 12px;
}
</style>

<!--<form v-on:submit.prevent="addItem">
  <div>
    <input id="itemForm" v-model="input" />
    <button v-on:click="addItem" v-bind:disabled="buttonDisabled">{{ buttonText }}</button>
  </div>
</form>
<ul>
  <li v-for="(dino,index) in items" v-bind:key="index">
    <h4>{{ dino.text }}</h4>
  </li>
</ul>


watch: {
  input: _.debounce(function () {
    this.buttonText = this.input !== '' ? 'Add ' + this.input : 'Add Dinosaur'
  }, 250)
},
methods: {
  addItem: function () {
    var input = document.getElementById('itemForm')
    if (input.value !== '') {
      this.items.push({
        text: input.value
      })
      input.value = ''
    }
  },
  addDino: function (index) {
    this.items[index].quantity++
  },
  minusDino: function (index) {
    this.items[index].quantity--
  },
  makeExtinct: function (index) {
    this.items.splice(index, 1)
  }
},
computed: {
  totalDinos: function () {
    this.dinosUpdated += 1
    let sum = 0
    let items = this.items
    for (let i in items) {
      sum += items[i].quantity
    }
    return sum
  },
  totalSpecies: function () {
    this.speciesUpdated += 1
    return this.items.length
  }
}
-->

<!--<ul>
  <li>
    Total Dinosaurus: {{ totalDinos }} <span>Updated: {{ dinosUpdated }}</span>
  </li>
  <li>
    Total Species: {{ totalSpecies }} <span>Updated: {{ speciesUpdated }}</span>
  </li>
</ul>-->
