<template>
  <div id="sponsors">
    <p>KHE is only possible due to the generosity of our sponsors. They're looking to work with passionate talent, just like you! Check them out!</p>
    <h1>Our sponsors:</h1>
    <div class="flex-container">
      <div v-for="(sponsor, index) in sponsors"
          class="sponsorWidget"
          :key="index">
        <a v-bind:href="sponsor.link"
            target="_blank">
        <br>
        <img v-bind:src="sponsor.imgUrl"
            class="sponsorImage"
            >
          </a>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Map',
    computed: {
      
    },
    mounted() {
      this.$parent.wrapper.sponsorSource.getSponsors()
        .then((data) => {
          this.sponsors = data;
          console.log("SPONSORS", this.sponsors)
        })
        .catch(console.error);
    },
    data() {
      return {
        sponsors: []
      };
    },
  };
</script>

<style scoped lang="scss">
  @import '@/globalVars.scss';

  #sponsors {
    padding: 100px 5vw 80px 5vw;
    padding-top: 50px;
    margin: 0px;
    text-align: left;
  }

  .sponsorImage {
    max-width: 300px;
    margin: 0 50px;
    filter: grayscale(100%);
  }

  .sponsorImage:hover {
    filter: grayscale(0%);
  }

  .flex-container {
    display: flex;
    flex-flow: row wrap;
    justify-content: space-around;
    align-items: center;
  }

  p {
    font-size: 20px;
    color: $dark-blue;
  }
</style>
