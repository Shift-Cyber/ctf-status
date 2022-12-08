<template>
  <div class="container">
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
  },
};
</script>

<style lang="scss" scoped>
.container {
  max-width:400px;
  margin: auto;

  margin-bottom: 100px;
}
</style>
