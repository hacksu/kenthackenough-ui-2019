<template>
  <div>
    <div id="map" class="widget">
      <div class="info-container">
        <div class="split">
            <h1>Where to Go:</h1>
            <p>Kent Hack Enough is graciously hosted in the Kent State Library, at: </p>
            <p>1125 Risman Dr, Kent, OH 44242</p>
            <h3>Parking</h3>
            <p>KSU will not be ticketing over the weekend. The two parking lots closest to the library are the Vistor Lot right by the bus stop, and the R lot by Eastway.</p>
        </div>
        
        <iframe class="split" id="mapIframe" src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3004.4427201307603!2d-81.34461668458171!3d41.14668997928703!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x88313accb4555555%3A0x3e830cbda94e6469!2sKent+State+University+Library!5e0!3m2!1sen!2sus!4v1510788212698" width="600" height="450" frameborder="0" style="border:0" allowfullscreen></iframe>
      </div>
    </div>
    
    <!--<div id="powered-by">
      <p id="powered-by-text">Powered By</p>

      <a id="small-hacksu-logo" href="http://hacksu.cs.kent.edu">
        <img id="powered-by-hacksu" src="../../assets/2018-hacksu-color.svg">
      </a>

      <a id="small-mlh-logo" href="https://mlh.io">
        <img id="powered-by-mlh" src="../../assets/mlh-logo.svg">
      </a>
    </div>-->
  </div>
</template>

<style scoped lang="scss">
  @import '@/globalVars.scss';

  #powered-by-text {
    color: #FF7E58;
    font-family: "Oswald", sans-serif;
    text-align: center;
    font-size: 20px;
    margin-top: 0px;
    margin-bottom: 10px;
  }

  #powered-by-hacksu {
    float: left;
    width: 50%;
    height: 90px;
  }

  #powered-by-mlh {
    float: right;
    width: 50%;
    height: 50px;
    margin-top: 17px;
  }

  #directions {
    text-align: left;
    flex: 1 1 500px;
    padding-right: 2rem;
  }

  #map {
    background: $blue;
    color: white;
  }

  .info-container {
    display: flex;
    flex-wrap: wrap;
    align-content: center;
    justify-content: space-between; 
    margin: 0 auto;
  }

  #mapIframe {
    flex: 1 1 500px;
    border-radius: 2%;
  }

  .widget {
    padding: 1rem;
  }

  p {
    font-size: 20px;
  }
  
  h3 {
    font-size: 22px;
  }

  .widget {
    padding: 20px;
  }

  .info-container {
    width: 100%;
    max-width: 1000px;
    margin: 0 auto;
  }

  .split {
    width: 100%;
    z-index: 1;
    text-align: left
  }

  @media screen and (min-width: 768px) {
    .widget {
      padding: 100px 100px 100px 100px;
    }
    
    .split {
      width: 50%;
    }

    #powered-by {
      display: flex;
      flex-direction: row;
      width: 100%;
      min-height: 50px;
      padding-left: 50px;
    }

    #powered-by-text {
      font-size: 18px;
      padding-top: 15px;
    }

    #powered-by-hacksu {
      width: 100%;
      height: 65px;
    }

    #powered-by-mlh {
      width: 100%;
      height: 65px;
      margin-top: 0;
    }

    #small-hacksu-logo {
      width: 150px;
    }

    #small-mlh-logo {
      width: 90px;
    }
  }

  @media screen and (max-width: 1199px) {
    .split {
      width: 100%;
    }
  }
</style>

<script>
export default {
  name: "Map",
  data() {
    return {};
  }
};
</script>
