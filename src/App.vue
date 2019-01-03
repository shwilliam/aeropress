<template>
  <div id='app'>
    <div class='intro'>
      <h1>AeroPress</h1>
      <p>
        Invented in 2005 by Alan Adler, the AeroPress is a relatively new coffee maker that is both lightweight and compact. It is a full immersion brew, like a French Press, but filtered with paper like a pour over, producing a clean and full-bodied cup of coffee.
      </p>
      <p class='instructions'>
        ↓<br /><br /><br /><br /><br /><br />
        ↓<br /><br /><br /><br /><br /><br />
        ↓
      </p>
    </div>

    <Scrollama
      :offset='0.5'
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
        3. Add about 200g of boiling water and carefully fit the plunger inside (preventing the coffee to drip through the filter)
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
      <div class='step' data-step-no='7'></div>
    </Scrollama>

    <div class='outro'>
      For more information about the AeroPress try this link, or this one. To get your own, check out the official website.
    </div>
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
      directionOfChange: null
    }
  },
  methods: {
    handleStepChange ({ element, index, direction }) {
      this.activeStep = element.dataset.stepNo
      this.directionOfChange = direction
    }
  }
}
</script>

<style src='vue-scrollama/dist/vue-scrollama.css'></style>
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-width: 620px;
}
.intro {
  padding-top: 15vh;
  padding-right: 5vw;
  padding-left: 10vw;
  padding-bottom: 10vh;
}
.intro p.instructions {
  padding-top: 17vh;
  text-align: center;
}
.outro {
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
</style>
