<template>
  <ClockDisplay />
  <CompetitionCategory v-for="(category, index) in $store.state.categories"
     :key="index" :category="category" />
</template>

<script>
import ClockDisplay from '@/components/ClockDisplay.vue';
import CompetitionCategory from '@/components/CompetitionCategory.vue';

export default {
  name: 'HomePage',
  components: {
    ClockDisplay,
    CompetitionCategory,
  },
};
</script>

<style lang="scss" scoped>
$base-color: #231F20
</style>
