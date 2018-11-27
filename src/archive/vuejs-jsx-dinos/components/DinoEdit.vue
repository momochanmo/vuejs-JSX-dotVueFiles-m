
<script>
export default { // eslint-disable-line no-new
  name: 'DinoEdit',
  props: ['initialQuantity', 'name'],
  data () {
    return {
      quantity: this.initialQuantity
    }
  },
  methods: {
    increment: function () {
      this.quantity += 1
    }
  },
  render (h) {
    return (
      <div id="dinoEdit">
        <button onClick={this.increment}>{this.quantity}</button>{this.name}
      </div>
    )
  }
}
</script>

<style scoped>

</style>

<!-- <style>


</style>
/* let DinoEdit = { // eslint-disable-line no-new
template: '#dinoEdit',
name: 'DinoEdit',
props: ['initialQuantity', 'name', 'index'],
data () {
return {
quantity: this.initialQuantity
}
},
methods: {
increment: function () {
this.quantity += 1
}
},
render (h) {
return (
<p>Hi this works</p>
)
}
} */
-->
