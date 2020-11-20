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
          <div v-html="$t(decisionTree[option].text)"></div>
        </div>
      </div>
    </div>
    <div
      v-if="previousChoice.length"
      class="d-flex justify-content-between my-4"
    >
      <button class="btn btn-light" @click="resetTest()">
        {{ $t('back_to_start_button') }}
      </button>
      <button class="btn btn-light" @click="goToPreviousChoice()">
        {{ $t('back_button') }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    previousChoice: [],
    initial: { options: [1, 2] },
    decisionTree: {
      1: {
        id: '1',
        text: 'votersGuide.label1',
        options: ['11', '12'],
      },
      11: {
        id: '11',
        text: 'votersGuide.label11',
        options: ['111', '112'],
      },
      111: {
        id: '111',
        text: 'votersGuide.label111',
        options: ['1110'],
      },
      1110: {
        id: '1110',
        text: 'votersGuide.label1110',
      },
      112: {
        id: '112',
        text: 'votersGuide.label112',
        options: ['1121', '1122'],
      },
      1121: {
        id: '1121',
        text: 'votersGuide.label1121',
        options: ['11210'],
      },
      11210: {
        id: '11210',
        text: 'votersGuide.label11210',
      },
      1122: {
        id: '1122',
        text: 'votersGuide.label1122',
        options: ['1122a', '1122b'],
      },
      '1122a': {
        id: '1122a',
        text: 'votersGuide.label1122a',
        options: ['1122a0'],
      },
      '1122b': {
        id: '1122b',
        text: 'votersGuide.label1122b',
        options: ['1122b0'],
      },
      '1122a0': {
        id: '1122a0',
        text: 'votersGuide.label1122a0',
      },
      '1122b0': {
        id: '1122b0',
        text: 'votersGuide.label1122b0',
      },
      12: {
        id: '12',
        text: 'votersGuide.label12',
        options: ['121', '122'],
      },
      121: {
        id: '121',
        text: 'votersGuide.label121',
        options: ['1210'],
      },
      1210: {
        id: '1210',
        text: 'votersGuide.label1210',
      },
      122: {
        id: '122',
        text: 'votersGuide.label122',
        options: ['1220'],
      },
      1220: {
        id: '1220',
        text: 'votersGuide.label1220',
      },
      2: {
        id: '2',
        text: 'votersGuide.label2',
        options: ['20'],
      },
      20: {
        id: '20',
        text: 'votersGuide.label20',
      },
    },
  }),
  methods: {
    goToPreviousChoice() {
      const previousOption = this.previousChoice.pop()
      this.initial.options = previousOption
    },
    goToNextChoice(option) {
      if (!this.decisionTree[option].options) {
        return
      }
      this.previousChoice.push(this.initial.options)
      this.initial.options = this.decisionTree[option].options
    },
    resetTest() {
      this.previousChoice = []
      this.initial.options = [1, 2]
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
