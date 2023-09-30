<template>
  <div id="app">
    <TitleBar :current="current" />
    <ScorerTable :scoreTable="scoreTable" :players="players" />
    <PassingSequence
      v-bind="{
        players,
        currentCount,
        passingSequence,
      }"
    />
    <ButtonContainer
      @pass="passHandler"
      @correct="correctHandler"
      @wrong="wrongHandler"
    />
  </div>
</template>

<script>
import TitleBar from './components/TitleBar.vue';
import ScorerTable from './components/ScorerTable.vue';
import PassingSequence from './components/PassingSequence.vue';
import ButtonContainer from './components/ButtonContainer.vue';
import { data } from './data/data';

export default {
  name: 'App',
  components: {
    TitleBar,
    ScorerTable,
    ButtonContainer,
    PassingSequence,
  },
  data() {
    return data;
  },
  methods: {
    passHandler() {
      this.currentCount++;
      if (this.currentCount >= 4) {
        this.moveNextQuestion();
      }
    },
    correctHandler(value) {
      const cp = this.passingSequence[this.currentCount];
      this.scoreTable.scores[cp] += value;
      if (this.currentCount > 0) {
        this.scoreTable.bonusAttempts[cp]++;
      }
      this.moveNextQuestion();
    },
    wrongHandler(value) {
      const cp = this.passingSequence[this.currentCount];
      if (value !== 5 || this.currentCount !== 3) {
        this.scoreTable.scores[cp] -= value;
      }
      this.currentCount++;
      if (this.currentCount === 4) {
        this.moveNextQuestion();
      }
    },
    moveNextQuestion() {
      console.log(
        `After question ${this.current.question} of player ${
          this.current.player + 1
        } in round ${this.current.round}:`
      );
      console.log(`Score are: ${this.scoreTable.scores}`);
      console.log(`BAs are: ${this.scoreTable.bonusAttempts}`);
      this.current.question++;
      this.currentCount = 0;
      if (this.current.question > 3) {
        this.current.player++;
        this.current.question = 1;
        if (this.current.player >= 4) {
          this.current.round++;
          this.current.player = 0;
        }
      }
      this.calculatePassingSequence();
    },
    calculatePassingSequence() {
      const passMap = {
        0: [1, 2, 3],
        1: [2, 3, 0],
        2: [3, 0, 1],
        3: [0, 1, 2],
      };

      this.passingSequence = [
        this.current.player,
        ...passMap[this.current.player].toSorted(
          (x, y) =>
            this.scoreTable.bonusAttempts[x] - this.scoreTable.bonusAttempts[y]
        ),
      ];
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
  box-sizing: border-box;
}
</style>
