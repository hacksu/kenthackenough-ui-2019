<template>
  <div id="landing-container">
    <div id="logo-container">
      <img src="@/assets/goldflourish.png" class="flipped"> 
          <!-- Note we're flipping this with CSS  so we don't have to load an extra asset! -->
      <img src="@/assets/goldshortlogo.png">
      <img src="@/assets/goldflourish.png">
      <br>
      <h1>KENT HACK ENOUGH</h1>
    </div>

    <!-- Art, absolutely positioned: -->
    <img src="@/assets/landing_assets/foreground_cliff.svg" id="foreground-cliff"
      class="desert-asset">
    <img src="@/assets/landing_assets/cowboy.svg" id="cowboy"
      class="desert-asset">

    <img src="@/assets/landing_assets/midground_1.svg" id="midground-1"
      class="desert-asset">
    <img src="@/assets/landing_assets/midground_2.svg" id="midground-2"
      class="desert-asset">
    <img src="@/assets/landing_assets/midground_3.svg" id="midground-3"
      class="desert-asset">

    <img src="@/assets/landing_assets/background_mesa.svg" id="mesa"
      class="desert-asset">
    <img src="@/assets/landing_assets/background_mountains.svg" id="mountains"
      class="desert-asset">

  </div>
</template>

<style scoped lang="scss">
@import '@/globalVars.scss';

#logo-container {

  height: 100px;
  margin-top: 100px;
  img {
    height: 100%;
    padding: 0px 10px;
  }
}
#landing-container {
  min-height: 100vh;
  overflow: hidden;
  padding: 0px;
  margin: 0px;
  padding-bottom: 20px;
  background: url('../assets/nightsky.png');
  background-size: cover;
  background-color: black;
  position: relative;
}

.desert-asset {
  position: absolute;
}
/* Note that for all positioning, we need to use 'vw' as our unit 
          -- even vertical positioning!!
        This way the assets will scale with the screen width, for mobile phones. */
#foreground-cliff {
  width: 60%;
  /* Slappin' a max-width on this bad boy bc otherwise it looks huge on a big screen */
  max-width: 700px;
  bottom: 0px;
  left: 0px;
  z-index: 10;
}
#cowboy {
  z-index: 9;
  width: 13%;
  bottom: 22vw;
  left: 25%;
  /* Using this media selector to make sure the cowboy stays on the cliff, even with it's max-width */
  @media only screen and (min-width: 1150px) {
    bottom: 260px;
    max-width: 150px;
  }
}

#midground-1 {
  right: -20px;
  bottom: -5vw;
  z-index: 9;
  width: 85%;
}
#midground-2 {
  right: -30px;
  bottom: 0px;
  z-index: 8;
  width: 85%;
}
#midground-3 {
  right: 0px;
  bottom: -2vw;
  z-index: 7;
}
#mesa {
  width: 30%;
  bottom: 12vw;
  right: 10%;
  z-index: 6;
}
#mountains {
  width: 120%;
  right: -170px;
  bottom: -10vw;
}
  
  @keyframes fadein {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
</style>

<script>
export default {
  name: 'Main',
  data() {
    return {
    };
  },
};
</script>