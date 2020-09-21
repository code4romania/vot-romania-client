<template>
  <div>
    <h2 class="text-center h4">
      {{ $t('guide_title') }}
    </h2>
    <div
      class="d-flex flex-column flex-sm-row justify-content-center align-items-center align-items-sm-stretch mt-3"
    >
      <div
        v-for="option in initial.options"
        :key="option"
        class="card"
        :class="{
          'choice-card text-center my-2 mx-0 mx-sm-2 font-weight-bolder':
            decisionTree[option].options,
        }"
        @click="goToNextChoice(option)"
      >
        <div class="card-body d-flex align-items-center justify-content-center">
          <p class="my-0" v-html="$t(decisionTree[option].text)"></p>
        </div>
      </div>
    </div>
    <div
      v-if="previousChoice.length"
      class="d-flex justify-content-between my-4"
    >
      <button class="btn btn-light" @click="resetTest()">
        Reseteaza testul
      </button>
      <button class="btn btn-light" @click="goToPreviousChoice()">
        Inapoi
      </button>
    </div>
  </div>
</template>
<script>
export default {
  data: () => ({
    previousChoice: [],
    initial: { options: [0, 1] },
    decisionTree: {
      0: {
        id: '0',
        text: 'votersGuide.label0',
        options: ['00', '01'],
      },
      1: {
        id: '1',
        text: 'votersGuide.label1',
        options: ['10', '11'],
      },
      '00': {
        id: '00',
        text: 'votersGuide.label00',
        options: ['000'],
      },
      '01': {
        id: '01',
        text: 'votersGuide.label01',
        options: ['010', '011'],
      },
      '000': {
        id: '000',
        text: 'votersGuide.label000',
      },
      '010': {
        id: '010',
        text: 'votersGuide.label010',
        options: ['0100'],
      },
      '0100': {
        id: '0100',
        text: 'votersGuide.label0100',
      },
      '011': {
        id: '011',
        text: 'votersGuide.label011',
        options: ['0110', '0111'],
      },
      '0110': {
        id: '0110',
        text: 'votersGuide.label0110',
        options: ['01100'],
      },
      '01100': {
        id: '01100',
        text: 'votersGuide.label01100',
      },
      '0111': {
        id: '0111',
        text: 'votersGuide.label0111',
        options: ['01110', '01111'],
      },
      '01110': {
        id: '01110',
        text: 'votersGuide.label01110',
        options: ['011100'],
      },
      '011100': {
        id: '011100',
        text: 'votersGuide.label011100',
      },
      '01111': {
        id: '01111',
        text: 'votersGuide.label01111',
        options: ['011110'],
      },
      '011110': {
        id: '011110',
        text: 'votersGuide.label011110',
      },
      10: {
        id: '10',
        text: 'votersGuide.label10',
        options: ['100', '101'],
      },
      100: {
        id: '100',
        text: 'votersGuide.label100',
        options: ['1000'],
      },
      1000: {
        id: '1000',
        text: 'votersGuide.label1000',
      },
      101: {
        id: '101',
        text: 'votersGuide.label101',
        options: ['1010'],
      },
      1010: {
        id: '1010',
        text: 'votersGuide.label1010',
      },
      11: {
        id: '11',
        text: 'votersGuide.label11',
        options: ['110'],
      },
      110: {
        id: '110',
        text: 'votersGuide.label110',
      },
    },
  }),
  methods: {
    goToPreviousChoice() {
      const previousOption = this.previousChoice.pop()
      this.initial.options = previousOption
    },
    goToNextChoice(option) {
      this.previousChoice.push(this.initial.options)
      this.initial.options = this.decisionTree[option].options
    },
    resetTest() {
      this.previousChoice = []
      this.initial.options = ['0', '1']
    },
  },
}
</script>

<style scoped>
.choice-card {
  max-width: 18rem;
  width: 100%;
  border: 2px solid #352245;
  transition: 0.2s border;
  position: relative;
  overflow: hidden;
}
.choice-card::before {
  content: '';
  opacity: 0;
  background: #352245;
  position: absolute;
  top: -25px;
  right: -25px;
  width: 50px;
  height: 50px;
  transform: rotate(45deg);
  transition: 0.3s opacity;
}
.choice-card::after {
  content: '';
  opacity: 0;
  background: no-repeat url(../assets/check-on.svg);
  background-size: cover;
  position: absolute;
  top: -2px;
  right: -2px;
  width: 25px;
  height: 25px;
  transition: 0.3s opacity;
}
.choice-card:hover::before,
.choice-card:hover::after {
  opacity: 1;
}
.choice-card:hover {
  cursor: pointer;
  border: 2px solid #fc0;
}
</style>
