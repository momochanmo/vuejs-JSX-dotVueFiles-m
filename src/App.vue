
<script>
import DinoEdit from './components/DinoEdit.vue'
import DinoShow from './components/DinoShow.vue'

export default { // eslint-disable-line no-new
  name: 'App',
  functional: false,
  data () {
    return {
      title: 'Dinosaurs',
      input: '',
      currentView: 'DinoEdit',
      items: [
        { text: 'Tyrannosaurus', quantity: 5, diet: 'Carnivore' },
        { text: 'Triceratops', quantity: 4, diet: 'Herbivore' },
        { text: 'Stegosaurus', quantity: 6, diet: 'Herbivore' }
      ]
    }
  },
  methods: {
    toggle: function () {
      this.currentView = this.currentView === 'DinoEdit' ? 'DinoShow' : 'DinoEdit'
    }
  },
  computed: {
    editLabel: function () {
      return this.currentView === 'DinoEdit' ? 'Edit' : 'Show'
    }
  },
  render (h) {
    return (
      <div id="card">
        <header>{this.title}<span onClick={this.toggle} style={{ marginLeft: '10%' }}>{this.editLabel}</span></header>
        <ul>
          {this.items.map((item) => (
            <li>
              {this.currentView === 'DinoEdit'
                ? <DinoEdit name={item.text} initialQuantity={item.quantity} />
                : <DinoShow name={item.text} diet={item.diet} />
              }
            </li>
          )
          )}
        </ul>
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
