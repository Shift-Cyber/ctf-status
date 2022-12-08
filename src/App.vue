<template>
  <body>
    <router-view/>
  </body>
</template>

<style lang="scss">
$color-base: #231F20;
$color-text: #E0E4EB;

$color-yellow: #FDFD96;
$color-purple: #5B005C;
$color-blue-1: #00F7E7;
$color-blue-2: #2B769E;
$color-blue-3: #2E4281;
$color-blue-4: #182242;

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $color-text;
}

body {
  background-color: $color-base;
}
</style>
