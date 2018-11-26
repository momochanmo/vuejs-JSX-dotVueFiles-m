<template>
  <div id="dinoShow">
    <div>
      <strong>{{ name }}</strong> | {{ diet }}
    </div>
  </div>
</template>

<script>
export default {
  props: ['name', 'diet']
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
