<template>
  <div class="container">
    <div class="category-label">{{ category_label.toUpperCase() }}</div>
    <CompetitionChallenge v-for="value, index in category" :key=index :challenge=value />
  </div>
</template>

<script>
import CompetitionChallenge from '@/components/CompetitionChallenge.vue';

export default {
  name: 'CompetitionCategory',
  components: {
    CompetitionChallenge,
  },
  props: {
    category: Array,
    category_label: String,
  },
};
</script>

<style lang="scss" scoped>
$color-base: #231F20;
$color-text: #E0E4EB;

$color-yellow: #FDFD96;
$color-purple: #5B005C;
$color-blue-1: #00F7E7;
$color-blue-2: #2B769E;
$color-blue-3: #2E4281;
$color-blue-4: #182242;

.container {
  max-width:205px;
  margin: auto;
  margin-bottom: 10px;

  border: 3px solid $color-yellow;
  border-radius: 10px;

  padding: 10px;
  padding-bottom: 0;
  margin: 10px;
}

.category-label {
  font-size: 12px;
  position: relative;
  transform: translateY(-17px);

  background: $color-base;
  color: $color-yellow;

  max-width: max-content;
  margin: 0 auto;
  padding: 0 7px;

  margin-bottom: -10px;
}
</style>
