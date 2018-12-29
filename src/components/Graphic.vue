<template>
  <div id='graphic'></div>
</template>

<script>
import * as SVG from 'svg.js'
import aeropressBottom from '@/assets/aeropress-bottom'
import aeropressTop from '@/assets/aeropress-top'
import aeropressFilterHolder from '@/assets/aeropress-filter_holder'

const scaleFactor = 0.3

export default {
  name: 'graphic',
  props: ['stepData'],
  data () {
    return {
      width: 300,
      height: 400
    }
  },
  mounted () {
    this.container = SVG('graphic')
      .size(this.width, this.height)

    this.aeropressFilterHolder = this.container
      .path(aeropressFilterHolder)
      .scale(scaleFactor)
      .fill('#000')
      .stroke({ color: '#000', width: '10px' })
      .move(100, 800)

    this.aeropressFilter = this.container
      .ellipse(100, 10)
      .radius(110.769, 10.787)
      .scale(scaleFactor)
      .fill('none')
      .stroke({ color: '#000', width: '5px' })
      .move(258, 670)

    this.aeropressBottom = this.container
      .path(aeropressBottom)
      .scale(0.3)
      .fill('none')
      .stroke({ color: '#000', width: '10px' })
      .move(-56.5, -400)

    this.coffeeCupTop = this.container
      .ellipse(100, 10)
      .radius(140.01, 8.42)
      .fill('none')
      .scale(scaleFactor)
      .stroke({ color: '#000', width: '7px' })
      .move(228, 1850)

    this.coffeeCupBottom = this.container.path('M5.013,14.356l4.179,311.575c90.751,36.439 182.61,38.89 275.816,0l0,-311.984 M284.994,88.291c80.103,-53.298 95.438,185.143 0.085,140.66')
      .fill('none')
      .scale(scaleFactor)
      .stroke({ color: '#000', width: '7px' })
      .move(-70.7, 1439)

    this.aeropressTop = this.container
      .path(aeropressTop)
      .scale(scaleFactor)
      .fill('none')
      .stroke({ color: '#000', width: '10px' })
      .move(-13, -1000)

    this.stick = this.container
      .line(146, 0, 146, 120)
      .stroke({ color: '#000', width: '3px' })
      .move(146, -1000)
  },
  watch: {
    stepData: function ({ activeStep, directionOfChange }) {
      this[`step${activeStep}`](directionOfChange)
    }
  },
  methods: {
    step1 (directionOfChange) {
      let aeropressFilterNextYPos = 850
      if (directionOfChange === 'up') aeropressFilterNextYPos = 670

      this.aeropressFilter
        .animate()
        .move(258, aeropressFilterNextYPos)

      let aeropressBottomNextYPos = -48
      if (directionOfChange === 'up') aeropressBottomNextYPos = -400

      this.aeropressBottom
        .animate()
        .move(-56.5, aeropressBottomNextYPos)
    },
    step2 (directionOfChange) {
      let nextYPosCoffeeCupTop = 850
      let nextYPosCoffeeCupBottom = 439
      if (directionOfChange === 'up') {
        nextYPosCoffeeCupTop = 1850
        nextYPosCoffeeCupBottom = 1439
      }

      this.coffeeCupTop
        .animate()
        .move(228, nextYPosCoffeeCupTop)

      this.coffeeCupBottom
        .animate()
        .move(-70.7, nextYPosCoffeeCupBottom)
    },
    step3 (directionOfChange) {
      let nextYPos = -470
      if (directionOfChange === 'up') nextYPos = -1000

      this.aeropressTop
        .animate()
        .move(-13, nextYPos)
    },
    step4 (directionOfChange) {
      let nextYPos = -1000
      if (directionOfChange === 'up') nextYPos = -470

      this.aeropressTop
        .animate()
        .move(-13, nextYPos)
    },
    step5 (directionOfChange) {
      let nextYPos = 100
      if (directionOfChange === 'up') {
        nextYPos = -1000
      } else {
        this.stick
          .animate()
          .move(146, nextYPos)

        this.stick
          .animate()
          .rotate(1)

        this.stick
          .animate()
          .rotate(-1)

        this.stick
          .animate()
          .rotate(1)

        this.stick
          .animate()
          .rotate(0)
      }
    },
    step6 (directionOfChange) {
      let nextYPos = -470
      if (directionOfChange === 'up') nextYPos = -1000

      this.stick
        .animate()
        .move(146, -1000)

      this.aeropressTop
        .animate()
        .move(-13, nextYPos)

      this.aeropressTop
        .animate({ delay: '0.4s' })
        .move(-13, -175)
    },
    step7 (directionOfChange) {
      let yMoveAmount = -2000
      if (directionOfChange === 'up') yMoveAmount = -0

      this.aeropressTop
        .animate()
        .dmove(0, yMoveAmount)
      this.aeropressBottom
        .animate()
        .dmove(0, yMoveAmount)
      this.aeropressFilterHolder
        .animate()
        .dmove(0, yMoveAmount)
      this.aeropressFilter
        .animate()
        .dmove(0, yMoveAmount)
    }
  }
}
</script>

<style scoped>
</style>
