<template>
  <div class="pass-container">
    <span v-for="(p, i) in getPassingSequence">
      <span v-if="i != 0"> {{ ' > ' }}</span>
      <span :class="{ active: currentCount === i, player: true }">
        {{ p }}
      </span>
    </span>
  </div>
</template>

<script>
export default {
  name: 'PassingSequence',
  props: ['passingSequence', 'players', 'currentCount'],
  computed: {
    getPassingSequence() {
      return this.passingSequence.map((x) => this.players[x].name || x + 1);
    },
  },
  methods: {},
};
</script>

<style scoped>
.pass-container {
  margin: 35px;
  line-height: 40px;
}
.player {
  padding: 5px 15px;
}

.active {
  border: 1px solid black;
  /* text-decoration: underline; */
  background-color: lightgrey;
  border-radius: 10px;
  font-weight: bold;
}
</style>
