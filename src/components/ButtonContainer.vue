<template>
  <div class="button-container">
    <div class="c1">
      <input
        type="button"
        class="pass-button"
        value="Pass"
        @click="passHandler"
      />
    </div>
    <div class="c2">
      <input
        type="button"
        value="Stake 5"
        @click="stakeHandler(5)"
        :class="{ staked: stakeValue === 5 }"
      />
      <input
        type="button"
        value="Stake 10"
        @click="stakeHandler(10)"
        :class="{ staked: stakeValue === 10 }"
      />
      <input
        type="button"
        value="Stake 20"
        @click="stakeHandler(20)"
        :class="{ staked: stakeValue === 20 }"
      />
    </div>
    <div class="c3">
      <input
        type="button"
        value="Correct"
        class="correct-button"
        @click="correctHandler"
        :disabled="stakeValue === 0"
      />
      <input
        type="button"
        value="Wrong"
        @click="wrongHandler"
        class="wrong-button"
        :disabled="stakeValue === 0"
      />
    </div>
    <div class="c4">
      <input type="button" value="Reset Question" disabled />
    </div>
  </div>
</template>

<script>
export default {
  name: 'ButtonContainer',
  data() {
    return {
      stakeValue: 0,
    };
  },
  methods: {
    stakeHandler(x) {
      this.stakeValue = this.stakeValue === x ? 0 : x;
    },
    passHandler() {
      this.stakeValue = 0;
      this.$emit('pass');
    },
    correctHandler() {
      this.$emit('correct', this.stakeValue);
      this.stakeValue = 0;
    },
    wrongHandler() {
      this.$emit('wrong', this.stakeValue);
      this.stakeValue = 0;
    },
  },
};
</script>

<style scoped>
.button-container {
  width: 50%;
  margin: auto;
}

.pass-button {
  width: 100%;
}

.c1 {
  margin-bottom: 10px;
}

.c2 {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 5px;
  margin-bottom: 10px;
}

.c3 {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 5px;
  margin-bottom: 30px;
}

input[type='button'] {
  cursor: pointer;
  height: 40px;
  font-size: 20px;
}

input:not([disabled]).correct-button {
  background-color: #45fd5c;
}

input:not([disabled]).wrong-button {
  background-color: #f37a76;
}

.staked {
  background-color: yellow;
}

.hide-button {
  visibility: hidden;
}
</style>
