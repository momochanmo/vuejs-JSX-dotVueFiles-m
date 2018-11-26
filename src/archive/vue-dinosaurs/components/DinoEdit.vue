<template>
  <div id="dinoEdit">
    <div>
      <button @click="increment">{{ quantity }}</button>{{ name }}
    </div>
  </div>
</template>


<script>
export default {
  props: ['initialQuantity', 'name', 'index'],
  data () {
    return {
      quantity: this.initialQuantity
    }
  },
  methods:{
    increment: function () {
      this.quantity += 1
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
