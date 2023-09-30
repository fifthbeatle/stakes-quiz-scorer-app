<template>
  <div class="title-bar">
    <span class="title-component">Round {{ current.round }} </span>
    <span class="title-component">Player {{ current.player + 1 }}</span>
    <span class="title-component question-number"
      >Question {{ current.question }}</span
    >
  </div>
</template>

<script>
export default {
  name: 'TitleBar',
  props: ['current'],
};
</script>

<style scoped>
.title-bar {
  margin-bottom: 25px;
  background-color: lightgrey;
  padding: 15px;
}

.title-component {
  margin: 0 10px;
}

.question-number {
  font-weight: bold;
}
</style>
