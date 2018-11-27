
<script>
export default { // eslint-disable-line no-new
  name: 'PracticeI',
  data () {
    return {
      counter: 0,
      textValue: '',
      showSpan: false,
      textValue2: '',
      showPs: false,
      renderT: false,
      paragraphs: []
    }
  },
  methods: {
    method1 () {
      this.counter++
      console.log(this.counter)
      this.showSpan = true
    },
    textChanged: function (event) {
      this.textValue = event.target.value
      this.showSpan = false
    },
    text2Changed: function (event) {
      this.textValue2 = event.target.value
    },
    showParagraphs: function () {
      this.showPs = true
    }// ,
    /* displayParagraphs: function (h) {
      const text = this.textValue2
      if (this.showPs) {
        this.paragraphs.push(text)
        this.textValue2 = ''
        this.showPs = false
        this.renderT = true
      }
      if (this.renderT) {
        return (
          <div>
            {this.paragraphs.map((paragraph) => (
              <p>{paragraph + ' ## ;p ^^ ¤¤ ;p # '}</p>
            ))}
          </div>
        )
      }
    } */
  },
  render (h) {
    let displayParagraphs = function () {
      const text = this.textValue2
      if (this.showPs) {
        this.paragraphs.push(text)
        this.textValue2 = ''
        this.showPs = false
        this.renderT = true
      }
      if (this.renderT) {
        return (
          <div>
            {this.paragraphs.map((paragraph) => (
              <p>{paragraph + ' ## ;p ^^ ¤¤ ;p ## '}</p>
            ))}
          </div>
        )
      }
    }
    displayParagraphs = displayParagraphs.bind(this)

    return (
      <div id="practiceI">
        <form name="f1">
          <input type="text" value={this.textValue} onInput={this.textChanged} />
          <button type="submit" onClick:prevent={this.method1}>Click</button>
          <span v-show={this.showSpan}>{this.textValue + ' ¤¤ ' + this.counter}</span>
        </form>
        <br /><br />
        <input id="tv2" type="text" placeholder="Type a paragraph using ' ' into it"
          onKeyup:k32={this.showParagraphs} value={this.textValue2} onInput={this.text2Changed}/>
        <br /><br />
        {displayParagraphs()}
      </div>
    )
  }
}
</script>

<style scoped>
  #tv2 {
    width: 300px;
  }
</style>
