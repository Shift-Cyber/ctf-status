<template>
  <div class="whole-element">
    <p class="clockface">{{ state.mainClock }}</p>
    <p class="status-label">{{ state.status }}</p>

    <div class="progress-bar total main-border">
      <div class="progress-bar completed" :style="{ width: state.completionPercentage }" />
    </div>

    <div class="progress-bar labels">
        <div class="progress-bar labels spent-time">{{ state.sinceStartClock }}</div>
        <div class="progress-bar labels spent-time">{{ state.completionPercentage }}</div>
        <div class="progress-bar labels spent-time">{{ state.untilEndClock }}</div>
    </div>
  </div>
</template>

<script>
import { reactive } from 'vue';

const startTime = 1670527670;
const endTime = 1671637670;

export default {
  name: 'ClockDisplay',
  setup() {
    const state = reactive({
      mainClock: '',
      status: '~~',
      sinceStartClock: '',
      untilEndClock: '',
      completionPercentage: '',
    });

    return {
      state,
    };
  },
  mounted() {
    this.state.mainClock = 'T-~~:~~:~~:~~';

    setInterval(() => {
      const dateTimeNow = Math.floor(Date.now() / 1000);

      this.setMainTime(dateTimeNow);
      this.setDuringCompetition(dateTimeNow);
    }, 1000);
  },
  methods: {
    setMainTime(dateTimeNow) {
      let posNeg = '';
      let days = '';
      let hours = '';
      let mins = '';
      let secs = '';

      if (startTime > dateTimeNow) {
        // time until start
        const timeDifference = startTime - dateTimeNow;

        posNeg = '-';
        days = Math.floor(timeDifference / (3600 * 24));
        hours = Math.floor((timeDifference % (3600 * 24)) / 3600);
        mins = Math.floor((timeDifference % 3600) / 60);
        secs = Math.floor(timeDifference % 60);

        this.state.status = 'COMPETITION IS STARTING SOON';
      } else {
        // time after start
        const timeDifference = dateTimeNow - startTime;

        posNeg = '+';
        days = Math.floor(timeDifference / (3600 * 24));
        hours = Math.floor((timeDifference % (3600 * 24)) / 3600);
        mins = Math.floor((timeDifference % 3600) / 60);
        secs = Math.floor(timeDifference % 60);

        this.state.status = 'COMPETITION IS LIVE';
      }

      if (dateTimeNow >= endTime) {
        this.state.status = 'COMPETITION IS OVER';
      }

      // force double digit entries
      days = days.toLocaleString('en-US', {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });

      hours = hours.toLocaleString('en-US', {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });

      mins = mins.toLocaleString('en-US', {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });

      secs = secs.toLocaleString('en-US', {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });

      this.state.mainClock = `T${posNeg}${days}:${hours}:${mins}:${secs}`;
    },
    setDuringCompetition(dateTimeNow) {
      let days = '';
      let hours = '';
      let mins = '';
      let secs = '';

      // left time should be the time since started
      let consumedTime = dateTimeNow - startTime;
      if (consumedTime > (endTime - startTime)) {
        consumedTime = endTime - startTime;
      }

      days = Math.floor(consumedTime / (3600 * 24));
      hours = Math.floor((consumedTime % (3600 * 24)) / 3600);
      mins = Math.floor((consumedTime % 3600) / 60);
      secs = Math.floor(consumedTime % 60);

      // force double digit entries
      days = days.toLocaleString('en-US', {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });

      hours = hours.toLocaleString('en-US', {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });

      mins = mins.toLocaleString('en-US', {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });

      secs = secs.toLocaleString('en-US', {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });

      this.state.sinceStartClock = `${days}:${hours}:${mins}:${secs}`;

      // right time is time until completed
      let remainingTime = endTime - dateTimeNow;
      if (remainingTime < 0) {
        remainingTime = 0;
      }

      days = Math.floor(remainingTime / (3600 * 24));
      hours = Math.floor((remainingTime % (3600 * 24)) / 3600);
      mins = Math.floor((remainingTime % 3600) / 60);
      secs = Math.floor(remainingTime % 60);

      // force double digit entries
      days = days.toLocaleString('en-US', {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });

      hours = hours.toLocaleString('en-US', {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });

      mins = mins.toLocaleString('en-US', {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });

      secs = secs.toLocaleString('en-US', {
        minimumIntegerDigits: 2,
        useGrouping: false,
      });

      this.state.untilEndClock = `${days}:${hours}:${mins}:${secs}`;

      // percentage is percentage of completion
      const totalCompetitionTime = endTime - startTime;
      const completionPercentage = Math.floor((consumedTime / totalCompetitionTime) * 100);

      this.state.completionPercentage = `${completionPercentage}%`;
    },
  },
};
</script>

<style lang="scss" scoped>
@font-face{
 font-family:'digital-clock-font';
 src: url('@/assets/digital.mono.ttf');
}

$color-base: #231F20;
$color-text: #E0E4EB;

$color-yellow: #FDFD96;
$color-purple: #5B005C;
$color-blue-1: #00F7E7;
$color-blue-2: #2B769E;
$color-blue-3: #2E4281;
$color-blue-4: #182242;

.whole-element {
  width: 425px;
  margin: 30px auto;
}

.clockface {
  font-family: 'digital-clock-font', Fallback, sans-serif;
  font-variant-numeric: tabular-nums lining-nums;
  font-size: 70px;

  color: $color-yellow;

  margin-top: -10px;
  margin-bottom: -10px;
}

.status-label {
  margin-top: 30px;
}

.progress-bar {
  height:15px;
  border-radius: 3px;

  &.main-border {
  }

  &.completed {
    background-color: $color-blue-2;
  }

  &.total {
    background-color: $color-blue-3;
  }

  &.labels {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin: 2px 0;
    color: $color-yellow;

    font-family: 'digital-clock-font', Fallback, sans-serif;
    font-size: 20px;

    &.spent-time {
      text-align:left;
    }

    &.remaining-time {
      text-align:right;
    }
  }
}
</style>
