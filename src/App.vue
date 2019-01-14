<template>
  <div id='app' :class='windowWidth < breakpoint ? "small" : null'>
    <header>
      <h1>AeroPress</h1>
      <p>
        Invented in 2005 by Alan Adler, the AeroPress is a relatively new coffee maker that is both lightweight and compact. It is a full immersion brew, like a French Press, but filtered with paper like a pour over, producing a clean and full-bodied cup of coffee.
      </p>
      <p class='instructions'>
        ↓<br /><br /><br /><br /><br /><br />
        ↓<br /><br /><br /><br /><br /><br />
        ↓
      </p>
    </header>

    <main>
      <Scrollama
        :offset='windowWidth < breakpoint ? 0.6 : 0.5'
        @step-enter='handleStepChange'
      >
        <div class='graphic' slot='graphic'>
          <Graphic :stepData='{activeStep, directionOfChange}' />
        </div>
        <div class='step' data-step-no='1'>
          1. Fit a filter paper in the filter holder and attach it to the bottom of your AeroPress chamber
        </div>
        <div class='step' data-step-no='2'>
          2. Place the AeroPress on top of your coffee cup/jug and pour about 15g of your favorite ground coffee inside
        </div>
        <div class='step' data-step-no='3'>
          3. Add about 200g of boiling water and carefully fit the plunger inside (preventing the coffee from dripping through the filter)
        </div>
        <div class='step' data-step-no='4'>
          4. After about 1 minute, remove the plunger and give your coffee a good stir
        </div>
        <div class='step' data-step-no='5'>
          5. Replace the plunger and let it brew for about another minute
        </div>
        <div class='step' data-step-no='6'>
          6. Gently and slowly press the plunger down until all of the coffee has been pushed through the filter
        </div>
        <div class='step' data-step-no='7'>
          7. Enjoy your freshly brewed cup of coffee
        </div>
      </Scrollama>
    </main>

    <footer>
      For more information about the AeroPress try <a href="http://nordiccoffeeculture.com/what-is-the-best-way-to-brew-aeropress-coffee/" target="_blank" rel="noopener noreferrer">this link</a>, or <a href="https://www.stumptowncoffee.com/brew-guides/aeropress" target="_blank" rel="noopener noreferrer">this one</a>. To get your own, check out <a href="https://aeropressinc.com/" target="_blank" rel="noopener noreferrer">the official website</a>.
    </footer>
  </div>
</template>

<script>
import 'intersection-observer'
import Scrollama from 'vue-scrollama'

import Graphic from '@/components/Graphic.vue'

// scroll to top on reload
window.scrollTo(0, 0)

export default {
  name: 'app',
  components: {
    Scrollama,
    Graphic
  },
  data () {
    return {
      activeStep: null,
      breakpoint: 700,
      directionOfChange: null,
      windowWidth: null
    }
  },
  methods: {
    handleStepChange ({ element, index, direction }) {
      this.activeStep = element.dataset.stepNo
      this.directionOfChange = direction
    },
    updateWindowWidth () {
      this.windowWidth = window.innerWidth
    }
  },
  mounted () {
    this.updateWindowWidth()
    window.addEventListener('resize', this.updateWindowWidth)
  },
  beforeDestroy () {
    window.removeEventListener('resize', this.updateWindowWidth)
  }
}
</script>

<style src='vue-scrollama/dist/vue-scrollama.css'></style>
<style>
html {
  background-color: #fffcf2;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 960px;
  margin: 0 auto;
  line-height: 24px;
}
header {
  padding-top: 10vh;
  padding-right: 6vw;
  padding-left: 10vw;
  padding-bottom: 10vh;
}
header h1 {
  font-size: 70px;
}
p.instructions {
  padding-top: 17vh;
  text-align: center;
}
footer {
  padding: 0 20vh 20vh 20vh;
}
.scrollama-container {
  display: flex;
}
.scrollama-container .scrollama-graphic {
  flex: 1;
  height: 80vh;
  top: 10vh;
}
.scrollama-container .scrollama-steps {
  flex: 1;
}
.graphic {
  height: 100%;
  margin: 0 3rem;
  display: flex;
  align-items: center;
  justify-content: center;
}
.step {
  padding: 0 0 40vh 0;
  margin: 20vh 2rem 0 .3rem;
  margin-bottom: 10vh;
  display: flex;
  align-items: center;
}
.step:first-of-type {
  margin-top: 30vh;
}
.step:last-of-type {
  margin-bottom: 0;
}
a {
  color: #000;
}
#app.small {
  padding-top: 40px;
  width: 340px;
}
#app.small header {
  padding: 30px 0 40px 0;
}
#app.small header h1 {
  font-size: 45px;
}
#app.small header .instructions {
  position: relative;
  left: -6px;
}
#app.small .scrollama-graphic, .graphic {
  background-color: #fffcf2;
  z-index: 2;
}
#app.small .scrollama-container .scrollama-graphic {
  height: 380px;
  top: -60px;
  padding-top: 100px;
  padding-bottom: 30px;
}
#app.small .scrollama-graphic > * {
  position: relative;
  left: -28px;
}
#app.small .scrollama-steps {
  position: relative;
  top: 0;
  left: -380px;
}
#app.small .scrollama-steps > * {
  width: 290px;
}
#app.small .step {
  padding: 120px 0 10px 0;
  margin: 0;
}
#app.small .step:first-of-type {
  margin-top: 446px;
}
#app.small footer {
  padding: 160px 0 180px 0;
}
</style>
