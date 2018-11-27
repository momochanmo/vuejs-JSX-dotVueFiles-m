
<script>
import PracticeI from './components/PracticeI.vue'

export default { // eslint-disable-line no-new
  name: 'App',
  functional: false,
  render (h) {
    return (
      <div id="app">
        <PracticeI/>
      </div>
    )
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
