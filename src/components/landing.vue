<template>
  <div id="landing-container">

    <div id="logo-container">
      <img src="@/assets/goldflourish.png" class="flipped"> 
          <!-- Note we're flipping this with CSS  so we don't have to load an extra asset! -->
      <img src="@/assets/goldshortlogo.png">
      <img src="@/assets/goldflourish.png" class="desktop-only">
      <br>
      <img src="@/assets/goldlonglogo.png" id="short-logo">
    </div>

    <div id="landing-content-container">
      <p><b>September 27<sup>th</sup>-29<sup>th</sup> 2019</b></p>
      <p>Kent State Library</p>
      <br>
      <router-link tag="button" :to="{name: 'register'}" class="gold-clear-button">
        Register Now!
      </router-link>
      <br>
      <a class="gold-link" href="https://sponsor.khe.io" target="_blank">
        Interested in Sponsoring?
      </a>
    </div>

    <!-- Art, absolutely positioned.
        The :style tags used on these assets make the assets shift slightly with the mouse motion
                                  & the scroll, for a nice parallax effects -->
    <img src="@/assets/landing_assets/foreground_cliff.svg" id="foreground-cliff"
      :style="{
          'margin-bottom': -(scrollPos / 85) - (mouseY / 55) + 'px',
          'margin-left': (mouseX / 55) - 50 + 'px'
        }"
      class="desert-asset">
    <img src="@/assets/landing_assets/cowboy.svg" id="cowboy"
      :style="{
          'margin-bottom': -(scrollPos / 55) - (mouseY / 55) + 'px',
          'margin-left': (mouseX / 55) + 'px'
        }"
      class="desert-asset">

    <img src="@/assets/landing_assets/midground_1.svg" id="midground-1"
      :style="{
          'margin-bottom': -(scrollPos / 30) - (mouseY / 45) + 'px',
          'margin-right': -(mouseX / 65) + 'px'
        }"
      class="desert-asset">
    <img src="@/assets/landing_assets/midground_2.svg" id="midground-2"
      :style="{
          'margin-bottom': -(scrollPos / 18) - (mouseY / 75) + 'px',
          'margin-right': -(mouseX / 85) + 'px'
        }"
      class="desert-asset">
    <img src="@/assets/landing_assets/midground_3.svg" id="midground-3"
    :style="{
          'margin-bottom': -(scrollPos / 13) + 'px',
          'margin-right': (mouseX / 85) - 40 + 'px'
        }"
      class="desert-asset">

    <img src="@/assets/landing_assets/background_mesa.svg" id="mesa"
      :style="{
          'margin-bottom': -(scrollPos / 10) + (mouseY / 65) + 'px',
          'margin-right': (mouseX / 75) + 'px'
        }"
      class="desert-asset">
    <img src="@/assets/landing_assets/background_mountains.svg" id="mountains"
      :style="{
          'margin-bottom': -(scrollPos / 7) + (mouseY / 45) + 'px',
          'margin-right': (mouseX / 65) - 60 + 'px'
        }"
      class="desert-asset">

  </div>
</template>

<script>

export default {
  name: 'landing',
  data() {
    return {
      scrollPos: 0,
      mouseX: 0,
      mouseY: 0
    }
  },
  mounted() {
    console.log("hi")
    this.handleScroll();
    window.addEventListener('scroll', this.handleScroll);
    document.onmousemove = this.handleMouseMove;
  },
  methods: {
    handleScroll() {
      this.scrollPos = window.scrollY;
    },
    handleMouseMove(e) {
      this.mouseX = e.clientX;
      this.mouseY = e.clientY;
    }
  }
}
</script>

<style scoped lang="scss">
@import '@/globalVars.scss';

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

#logo-container {

  height: 130px;
  margin-top: 100px;
  img {
    height: 70%;
    padding: 0px 10px;
    @media only screen and (max-width: $md-bp) {
      height: 40%;
    }
  }
  #short-logo {
    margin-top: 20px;
    width: 25vw;
    height: auto;
    @media only screen and (max-width: $md-bp) {
      width: 50vw;
    }
  }
}

#landing-content-container {
  margin-top: 80px;
  font-size: 2rem;
  z-index: 11;
  position: relative;
  color: $gold;
  font-family: athelas;
  p {
    margin: 10px;
  }
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
  bottom: -1vw;
  z-index: 8;
  width: 85%;
}
#midground-3 {
  right: 0px;
  bottom: -6vw;
  z-index: 7;
}
#mesa {
  width: 30%;
  bottom: 8vw;
  right: 10%;
  z-index: 6;
}
#mountains {
  width: 120%;
  right: -170px;
  bottom: -16vw;
}
  
  @keyframes fadein {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }

  sup {
    font-size: 14px;
  }
</style>