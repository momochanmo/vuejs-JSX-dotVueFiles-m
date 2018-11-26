<template>
  <div id="dinoCounter">
    <div>
      <button @click="increment">{{ quantity }}</button>{{ name }}
    </div>
  </div>
</template>


<script>
export default {
  props: ['name', 'initialQuantity'],
  data () {
    this.$emit('increment', this.initialQuantity)
    return {
      quantity: this.initialQuantity
    }
  },
  methods:{
    increment: function () {
      this.quantity += 1
      console.log(this.quantity)
      this.$emit('increment', 1)
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
