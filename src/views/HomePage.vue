<template>
  <ClockDisplay />
  <Statuskey />
  <div class="category-container">
    <CompetitionCategory v-for="(category, category_label) in $store.state.categories"
     :key="category_label" :category="category" :category_label="category_label" />
  </div>
</template>

<script>
import ClockDisplay from '@/components/ClockDisplay.vue';
import Statuskey from '@/components/StatusKey.vue';
import CompetitionCategory from '@/components/CompetitionCategory.vue';
import store from '@/store';

export default {
  name: 'HomePage',
  components: {
    ClockDisplay,
    CompetitionCategory,
    Statuskey,
  },
  mounted() {
    store.commit('update_epoch_all');
  },
};
</script>

<style lang="scss" scoped>
.category-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
