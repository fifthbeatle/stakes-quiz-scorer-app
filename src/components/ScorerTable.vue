<template>
  <div class="container">
    <table class="labels">
      <tr>
        <td>Players</td>
      </tr>
      <tr>
        <td>Score</td>
      </tr>
      <tr>
        <td>BA</td>
      </tr>
    </table>
    <table class="score-table">
      <tr class="table-header">
        <th v-for="player in players" class="player-name-th">
          <input
            type="text"
            class="player-name-input"
            v-model="player.name"
            :placeholder="player.placeholder"
          />
        </th>
      </tr>
      <tr class="table-row">
        <td v-for="(player, i) in players">
          <input
            type="text"
            class="scores-ba"
            v-model.number="scoreTable.scores[i]"
          />
        </td>
      </tr>
      <tr class="table-row">
        <td v-for="(player, i) in players">
          <input
            type="text"
            class="scores-ba"
            v-model.number="scoreTable.bonusAttempts[i]"
          />
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'ScorerTable',
  props: ['scoreTable', 'players'],
  computed: {},
};
</script>

<style>
.container {
  display: flex;
}

.labels {
  flex: 1 1 auto;
}

.score-table {
  flex: 8 8 auto;
}

.labels tr {
  /* padding: 5px; */
  height: 40px;
  box-sizing: border-box;
  font-size: 20px;
  text-align: right;
  font-weight: bold;
}

.table-header {
  height: 40px;
}

.table-row {
  font-weight: bold;
  font-size: 20px;
}

.player-name-th {
  width: 20%;
}

.scores-ba {
  border: none;
  text-align: center;
  font-weight: bold;
  font-size: 18px;
  width: 100%;
}

.player-name-input {
  background-color: #eee;
  /* font-weight: bold; */
  width: 100%;
  padding: 5px;
  font-size: 14px;
  text-align: center;
  box-sizing: border-box;
}
</style>
