<template>
  <div id='app'>
    <div class='intro'>
      <h1>AeroPress</h1>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Soluta, at
        velit sint facere ipsam doloremque placeat vel impedit sapiente alias.
      </p>
      <p>SCROLL TO CONTINUE</p>
    </div>

    <Scrollama
      :offset='0.5'
      @step-enter='handleStepChange'
    >
      <div class='graphic' slot='graphic'>
        <Graphic :stepData='{activeStep, directionOfChange}' />
      </div>
      <div class='step' data-step-no='1'>step 1</div>
      <div class='step' data-step-no='2'>step 2</div>
      <div class='step' data-step-no='3'>step 3</div>
      <div class='step' data-step-no='4'>step 4</div>
    </Scrollama>

    <div class='outro'>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Soluta, at velit
      sint facere ipsam doloremque placeat vel impedit sapiente alias.
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
  margin-top: 60px;
}
.intro,
.outro {
  padding: 20vh;
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
  border: 1px solid #ccc;
  background-color: #eee;
  display: flex;
  align-items: center;
  justify-content: center;
}
.step {
  padding: 20vh 0;
  margin: 0 3rem;
  margin-bottom: 10vh;
  background-color: beige;
  border: 1px solid #ccc;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
