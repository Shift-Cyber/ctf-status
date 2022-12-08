<template>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.2.1/css/all.min.css" integrity="sha512-MV7K8+y+gLIBoVD59lQIYicR65iaqukzvf/nwasF0nqhPay5w/9lJmVM2hMDcnK1OnMGCdVK+iQrJ7lzPJQd1w==" crossorigin="anonymous" referrerpolicy="no-referrer" />

  <div class="challenge">
    <div class="tooltip">
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
      <span class="tooltiptext">{{ epochToHumanReadable(challenge.lastChecked) }}</span>
    </div>

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

/* Tooltip container */
.tooltip {
  position: relative;
  display: inline-block;
  border-bottom: 1px dotted black; /* If you want dots under the hoverable text */
}

/* Tooltip text */
.tooltip .tooltiptext {
  visibility: hidden;
  width: 120px;
  background-color: black;
  color: #fff;
  text-align: center;
  padding: 5px 0;
  border-radius: 6px;

  /* Position the tooltip text - see examples below! */
  position: absolute;
  z-index: 1;
}

/* Show the tooltip text when you mouse over the tooltip container */
.tooltip:hover .tooltiptext {
  visibility: visible;
}
</style>
