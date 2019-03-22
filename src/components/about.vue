<template>
<div id="about-container">
  <div id="header-container">
    <img src="@/assets/yeehaw.png">
    <img src="@/assets/goldflourish.png"> 

  </div>
  <div id="about-content-container">
    <img src="@/assets/about_page_assets/hat.svg">
    <div id="about-text-container">
       Listen here, buckaroo. You think you have what it takes for the rootin'-est, tootin'-est hackathon in the wild midwest?<br><br>
    </div>
  </div>
  <div id="colored-text-container">
    This is our 8th KHE! Whether you're <b>totally new</b> to tech & design or a <b>seasoned pro</b>, come spend a weekend making something great with us!
  </div>
</div>

</template>

<script>
export default {

}
</script>

<style scoped lang="scss">
@import '@/globalVars.scss';

#header-container {
  width: 70%;
  margin-top: 100px;
  margin-left: 5vw;
  padding-left: 5vw;
  text-align: left;
  img {
    height: 8vw;
    margin-right: 1vw;
  }
}
#about-container {
  min-height: 100vh;
  overflow: hidden;
  padding: 0px;
  margin: 0px;
  padding-bottom: 20px;
  background-size: cover;
  background-color: $dark-blue;
  position: relative;
}
#about-content-container {
  margin: 60px 10vw;
  display: flex;
  @media only screen and (max-width: $lg-bp) {
    flex-flow: column;
  }
  // height: 100%;
  img {
    width: 60vw;
    align-self: center;
  }
  justify-content: space-between;
}

#about-text-container {
  min-height: 200px;
  font-size: 30px;
  text-align: justify;
  padding: 5vw;
  line-height: 50px;
  margin-left: 10vw;
  color: $light-blue;
  @media only screen and (max-width: $lg-bp) {
    margin-left: 0vw;
    font-size: 20px;
    line-height: 30px;
  }
}
#colored-text-container {
  background: $gold;
  box-shadow: 10px 10px 0px $blue;
  font-size: 24px;
  text-align: left;
  color: $dark-blue;
  padding:  20px 5vw;
  margin: 0px 15vw 100px;
  @media only screen and (max-width: $lg-bp) {
    font-size: 18px;
  }
}
</style>