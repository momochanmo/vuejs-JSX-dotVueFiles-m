
<script>
export default { // eslint-disable-line no-new
  name: 'DinoShow',
  props: ['name', 'diet'],
  render (h) {
    return (
      <div id="dinoShow">
        <strong>{this.name}</strong> | {this.diet}
      </div>
    )
  }
}
</script>

<style scoped>

</style>
