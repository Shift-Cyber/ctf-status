<template>
  <div class="key-container">
    <div class="key">
        <i id=status class="fa-solid fa-circle healthy" />
        <p>Healthy</p>
    </div>

    <div />

    <div class="key">
        <i id=status class="fa-solid fa-circle degraded" />
        <p>Degraded</p>
    </div>

    <div />

    <div class="key">
        <i id=status class="fa-solid fa-circle down" />
        <p>Down</p>
    </div>

    <div />

    <div class="key">
        <i id=status class="fa-solid fa-circle disconnected" />
        <p>Solver-Issue</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'KeyContainer',
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

.key-container {
  width: 425px;
  margin: 30px auto;

  display: flex;
  flex-direction: row;
  justify-content: center;

  margin-bottom: 10px;
  margin-top: 40px;
}

.key {
    display: flex;
    flex-direction: row;
    align-items: center;

    margin: -20px 10px;

    & p {
        margin-top: 20px;
        margin-left: 5px;
    }
}

.healthy { color: green; }
.degraded { color: yellow; }
.down { color: red; }
.disconnected { color: grey; }
</style>
