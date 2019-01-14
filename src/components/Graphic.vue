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
      height: 400,
      stepsRan: []
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

    this.water = this.container.rect(56.5, 0)
      .fill('#c4e3ed')
      .x(117.5)
      .y(245.8)

    this.waterBottom = this.container.ellipse(55, 0)
      .fill('#c4e3ed')
      .x(118.2)
      .y(246)

    this.coffeeGroundsCoordinates = []
    const xAmount = 24
    const xInitial = 11
    const yEnd = 116
    const xSpace = 2.24
    const wideLayer = Array.from(Array(xAmount), (x, i) => {
      return {
        x: xInitial + (i * xSpace) + (Math.random() * 2),
        y: yEnd + (Math.random() * 0.6)
      }
    })

    const ySpace = 1.4
    const layers = 4
    Array(layers).fill(null)
      .forEach((layer, i) => {
        if (i === 0) {
          this.coffeeGroundsCoordinates.push(...wideLayer)
        } else {
          wideLayer.pop()
          this.coffeeGroundsCoordinates.push(
            ...wideLayer.map(({ x, y }) => {
              const newY = y + (ySpace * i) + (Math.random() * 2)
              const newX = x + (xSpace * (Math.random() * 1.2))
              return { x: newX, y: newY }
            })
          )
        }
      })

    this.coffeeGroundsCoordinates.forEach(({ x, y }, i) => {
      this.container.polygon('850,75  958,137.5 958,262.5 850,325 742,262.6 742,137.5')
        .fill('#000')
        .attr({ class: 'coffee-grounds' })
        .move(x, -500)
        .scale(0.015, 0.01)
    })
  },
  watch: {
    stepData: function ({ activeStep, directionOfChange }) {
      if (directionOfChange === 'down' && this.stepsRan.indexOf(activeStep) === -1) {
        this[`step${activeStep}`](directionOfChange)
        this.stepsRan.push(activeStep)
      }
    }
  },
  methods: {
    step1 () {
      this.aeropressFilter
        .animate()
        .move(258, 850)

      this.aeropressBottom
        .animate()
        .move(-56.5, -48)
    },
    step2 () {
      this.coffeeCupTop
        .animate()
        .move(228, 850)

      this.coffeeCupBottom
        .animate()
        .move(-70.7, 439)

      SVG.select('.coffee-grounds').members
        .forEach((el, i) => {
          el
            .animate()
            .move(0, (parseFloat(this.coffeeGroundsCoordinates[i].y) / 0.01) + (496 / 0.01))
        })
    },
    step3 () {
      this.water
        .animate()
        .height(70)
        .y(177)

      this.waterBottom
        .animate()
        .radius(28.3, 4.5)

      this.aeropressTop
        .animate()
        .move(-13, -470)
    },
    step4 () {
      this.stick
        .animate()
        .move(146, 100)

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

      this.aeropressTop
        .animate()
        .move(-13, -1000)

      this.water.animate().fill('#9f8574')

      this.waterBottom.animate().fill('#9f8574')

      SVG.select('.coffee-grounds').animate().opacity(0)
    },
    step5 () {
      this.stick
        .finish()
        .animate()
        .move(146, -1000)

      this.aeropressTop
        .animate()
        .move(-13, -470)
    },
    step6 () {
      this.aeropressTop
        .animate()
        .move(-13, -175)

      this.water
        .animate()
        .height(0)
        .y(244)

      this.waterBottom
        .animate()
        .y(244)
        .radius(28.3, 0)
    },
    step7 () {
      this.aeropressTop
        .finish()
        .animate()
        .dmove(0, -2000)

      this.aeropressBottom
        .animate()
        .dmove(0, -2000)

      this.aeropressFilterHolder
        .animate()
        .dmove(0, -2000)

      this.aeropressFilter
        .animate()
        .dmove(0, -2000)

      this.heatLeft = this.container
        .path('M10,10 L50,100 L90,50')
        .scale(scaleFactor)
        .stroke({ color: '#000', width: '6px' })
        .fill('none')
        .rotate(90)

      this.heatRight = this.container
        .path('M10,10 L50,100 L90,50')
        .scale(scaleFactor)
        .stroke({ color: '#000', width: '6px' })
        .fill('none')
        .rotate(90)

      const nums = []
      for (let i = 0; i < 100; i++) {
        nums.push(i)
      }
      let t = 0

      const animateHeat = () => {
        let points = nums.map(num => {
          const y = 100 + 10 * Math.sin((num + t) / 10)
          const x = num * 1.4
          return [x, y]
        })
        let pathLeft = `M${points.map(p => `${p[0] + 480},${p[1] - 300}`).join(' L')}`
        let pathRight = `M${points.map(p => `${p[0] + 480},${p[1] - 420}`).join(' L')}`
        this.heatLeft.attr({ d: pathLeft })
        this.heatRight.attr({ d: pathRight })
        t += 0.5
        requestAnimationFrame(animateHeat)
      }
      animateHeat()
    }
  }
}
</script>

<style scoped>
</style>
