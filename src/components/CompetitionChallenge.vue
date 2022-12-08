<template>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.2.1/css/all.min.css" integrity="sha512-MV7K8+y+gLIBoVD59lQIYicR65iaqukzvf/nwasF0nqhPay5w/9lJmVM2hMDcnK1OnMGCdVK+iQrJ7lzPJQd1w==" crossorigin="anonymous" referrerpolicy="no-referrer" />

  <div class="challenge">
    <div v-if="challenge.status === 'healthy'">
      <i id=status class="fa-solid fa-circle challenge status healthy" />
    </div>
    <div v-else-if="challenge.status === 'degraded'">
      <i id=status class="fa-solid fa-circle challenge status degraded" />
    </div>
    <div v-else-if="challenge.status === 'down'">
      <i id=status class="fa-solid fa-circle challenge status down" />
    </div>
    <div v-else-if="challenge.status === 'disconnected'">
      <i id=status class="fa-solid fa-circle challenge status disconnected" />
    </div>

    <b-tooltip target="tooltip-target-1" triggers="hover">
      {{ epochToHumanReadable(challenge.lastChecked) }}
    </b-tooltip>

    <div>{{ challenge.name }}</div>
  </div>
</template>

<script>
export default {
  name: 'CompetitionChallenge',
  props: {
    challenge: Object,
  },
  methods: {
    epochToHumanReadable(epoch) {
      const date = new Date(epoch * 1000);
      return date.toLocaleString();
    },
  },
};
</script>

<style lang="scss" scoped>
.challenge {
  display: flex;
  flex-direction: row;
  margin-bottom: 5px;

  &.status {
    margin-right: 5px;

    &.healthy { color: green; }
    &.degraded { color: yellow; }
    &.down { color: red; }
    &.disconnected { color: grey; }
  }

  &.time {
    font-size: 12px;
    line-height: 18px;
  }
}
</style>
