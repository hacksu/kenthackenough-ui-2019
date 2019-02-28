<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="scss">
@import '@/globalVars.scss';


@font-face {
  font-family: nandaka;
  src: url("./assets/fonts/nandaka_western.ttf");
}
@font-face {
  font-family: athelas;
  src: url("./assets/fonts/Athelas-Regular.ttf");
}

h1 {
  font-family: nandaka;
  color: $gold;
  font-size: 40px;
}


#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  position: absolute;
  width: 100%;
  top: 0px;
  left: 0px;
}
.flipped {
  transform: scaleX(-1);
}
</style>
