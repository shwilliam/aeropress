<template>
  <div id='graphic'></div>
</template>

<script>
import * as SVG from 'svg.js'

export default {
  name: 'graphic',
  props: ['stepData'],
  data () {
    return {
      width: 300,
      height: 300
    }
  },
  mounted () {
    this.container = SVG('graphic')
      .size(this.width, this.height)

    this.testShape = this.container
      .rect(100, 100)
      .move(0, -200)
      .attr({ fill: '#f06' })
  },
  watch: {
    stepData: function ({ activeStep, directionOfChange }) {
      this[`step${activeStep}`](directionOfChange)
    }
  },
  methods: {
    step1 (directionOfChange) {
      let yChange = 200
      if (directionOfChange === 'up') yChange = -Math.abs(yChange)

      this.testShape
        .animate()
        .move(0, yChange)
    },
    step2 () {
      console.log(2)
    },
    step3 () {
      console.log(3)
    },
    step4 () {
      console.log(4)
    }
  }
}
</script>

<style scoped>
</style>
