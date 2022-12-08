<template>
  <div class="whole-element">
    <p class="clockface">T-00:00:00:00</p>
    <p class="status-label">COMPETITION STARTING SOON</p>

    <div class="progress-bar total main-border">
      <div class="progress-bar completed"></div>
    </div>

    <div class="progress-bar labels">
        <div class="progress-bar labels spent-time">00:00:00:00</div>
        <div class="progress-bar labels spent-time">66%</div>
        <div class="progress-bar labels spent-time">00:00:00:00</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ClockDisplay',
};
</script>

<style lang="scss" scoped>
@font-face{
 font-family:'digital-clock-font';
 src: url('@/assets/digital.ttf');
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
  font-size: 80px;

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
    width:66%;
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
