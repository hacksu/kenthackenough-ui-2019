<template>
  <div id="app">
    <div id="banner">
      <div id="bannerL" class="bannerContainer">
        <p class="banner-link khe-link" id="kheTitle"
           @click="scrollTo('/', '#mainContainer')">KENT HACK ENOUGH</p>
        
        <div id="hamburgMenu">
          <img id="hamburgIcon" src="@/assets/Hamburger_icon.svg.png" width="50" @click="togMenu()">
        </div>
      </div>
      
      <div id="bannerR" class="bannerContainer" :class="{'hidden': expandMenu}">
        <p class="banner-link" @click="scrollTo('/', 'landing-container')">Home</p>
        <!-- <p class="banner-link"@click="scrollTo('/', '#about-container')">About</p> -->
        <p class="banner-link" @click="scrollTo('/', '#faq-container')">FAQ</p>
        <p class="banner-link" @click="scrollTo('/sponsor', '#sponsors')">Sponsors</p>
        <!-- <p class="banner-link" @click="navTo('/contact')">Contact</p> -->
        <!-- <p class="banner-link" @click="navTo('/schedule')">Schedule</p> -->
        <p class="banner-link" @click="scrollTo('/', '#map')">Map</p>
        <p class="banner-link" @click="scrollTo('/register', '#register')" v-if="user._id == ''">Register/Login</p>
        <p class="banner-link" @click='logout()' v-if="user._id != ''">Log out</p>
        <!-- <p class="banner-link" @click="navTo('/live')">Live!</p> @click="scrollTo('/', '#faq-container')"-->
        <div class="padding" style="width: 50px"></div>
      </div>
    </div>
    <router-view/>
  </div>
</template>

<script>
import { ApiWrapper } from "khe-frontend-lib";
import scrollto from "vue-scrollto";

import apiConfig from "./config/config";

export default {
  name: "app",
  components: {
  },
  data() {
    return {
      showLogin: false,
      showRegister: true,
      showPasswordReset: false,
      
      hasApp: false,
      hasCheckedForApp: false,
      expandMenu: false,
      user: this.userInitialState(),
      wrapper: new ApiWrapper(apiConfig),
      liveUpdates: {},
      events: [],
      messages: [],
      scores: []
    };
  },
  mounted() {
    // Checking if a user is saved as logged in
    var user = this.wrapper.userManager.getLocalUser();
    if (user && user.key) {
      console.log("You've been logged in from a previous session!");
      this.user._id = user.key;
      this.user.email = user.email;
      this.user.role = user.role;

      // Redirects to home if they're on register 
      if (this.$route.fullPath == '/register' || this.$route.fullPath == '/login') {
        this.$router.push('/')
      }
      
      // Checks if the user has an application
      this.wrapper.applicationManager.getApplication()
      .then((app) => {
        console.log("Hey you have an app: ", app);
        this.hasApp = app._onServer;
        this.hasCheckedForApp = true;
      }).catch((err) => {
        console.error("Problem getting your app!!");
        this.hasCheckedForApp = true;
      })
    }
    // LOADING IN SCHEDULE
    let vm = this;
        this.liveUpdates = this.wrapper.liveManager;
        this.liveUpdates.exisitingEvents().then((msgs) => {
            for (let i = 0; i < msgs.length; i++)
                vm.events.push(msgs[i])
        });
        this.liveUpdates.SubscribeToEvents({
            onCreate(event) {
                vm.events.unshift(event);
            },
            onUpdate: function(event) {
                var index = vm.events.findIndex(function(o){
                    return o._id === event._id;
                });
                vm.events.splice(index, 1);
                vm.events.push(event);
            },
            onDelete: function(event) {
                var index = vm.events.findIndex(function(o){
                    return o._id === event._id;
                });
                if (index !== -1) vm.events.splice(index, 1);
            }
        });
    // LOADING IN UPDATES
    this.liveUpdates.exisitingMessages().then((msgs) => {
      for (let i = 0; i < msgs.length; i++)
        vm.messages.push(msgs[i])
      });
      this.liveUpdates.SubscribeToMessages({
            onCreate(msg) {
                vm.messages.unshift(msg);
            },
            onUpdate: function(event) {
                var index = vm.messages.findIndex(function(o){
                    return o._id === event._id;
                });
                vm.messages[index].text = event.text;
            },
            onDelete: function(event) {
                var index = vm.messages.findIndex(function(o){
                    return o._id === event._id;
                });
                if (index !== -1) vm.messages.splice(index, 1);
            }
        });
    this.getScores();
  },
  methods: {
    dispLogin: function() {
      // Normally we could do a one line function like this inside an @click attribute,
      // but this makes it easier to access from it's children
      this.expandMenu = false;
      this.showLogin = !this.showLogin;
    },
    dispRegister: function() {
      this.expandMenu = false;
      this.showRegister = !this.showRegister;
    },
    dispPasswordReset: function() {
      this.expandMenu = false;
      this.showPasswordReset = false
    },
    switchLoginRegister: function() {
      this.showRegister = !this.showRegister;
      this.showLogin = !this.showLogin;
    },
    switchPasswordReset: function() {
      this.showLogin = false;
      this.showPasswordReset = !this.showPasswordReset;
    },
    getScores() {
      // LOADING LEADERBOARD:
      var vm = this;
        this.wrapper.gamifyV1.scoreboard()
        .then((scores) => {
            vm.scores = scores;
        })
        .catch((err) => {
            throw err;
        });
    },
    userInitialState() {
      this.hasApp = false;
      return {
        _id: "",
        email: "",
        //        password: '',
        key: "",
        role: "",
        application: {
          name: "", // full name                                      !
          school: "", // name of school                               !
          phone: "", // phone number                                  !
          shirt: "", // t-shirt size                                  !
          demographic: null, // allowed to use demographic info?       ?
          first: null, // is this your first hackathon?               !
          dietary: [], // food restrictions seperated by |            !
          // Vegan, vegitarian, kosher, gluten free, allergy, other
          year: "", // the year in school                             !
          age: '', // person's age                                    !
          gender: "", // gender                                       !
          major: "", // degree                                        !
          conduct: null, // agree to MLH code of conduct?              ?
          travel: null, // need travel reimbursement?                 !
          waiver: false, // agreed to waiver?                           ?
          resume: "", // the filename of their resume                   ?
          link: "", // a github/linkedin link                           ?
          extra: ""
        }
      };
    },
    logout: function() {
      this.wrapper.userManager.logout();
      //        .then(() => {
      //        console.log("Logged out!");
      //      }).catch((err) => {
      //        console.error("Error logging out: ", err);
      //      })
      this.user = this.userInitialState();
      this.$router.push({ path: "/" });
    },
    togMenu: function() {
      this.expandMenu = !this.expandMenu;
    },
    scrollTo: function(page, el) {
      this.expandMenu = false;
      if (this.$route.path !== page) {
        this.$router.push(page);
        this.scrollToEl = el;
      } else {
        scrollto.scrollTo(el, 300);
      }
    }
  }
};
</script>

<style lang="scss">
  @import '@/globalVars.scss';

  #hamburgMenu {
    display: none;
  }

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
    font-family: athelas;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    position: absolute;
    width: 100%;
    top: 0px;
    left: 0px;
  }

  #banner {
    /*position: fixed;*/
    background-color: $dark-blue;
    display: flex;
    justify-content: space-between;
    z-index: 98;
  }

  .banner-link {
    padding: 15px;
    margin: 0px;
    font-size: 18px;
    color: #fff;
    cursor: pointer;
    -webkit-transition-duration: 0.2s;
    transition-duration: 0.2s;
  }

  .banner-link:hover {
    background-color: $blue;
  }

  .bannerContainer {
    display: flex;
  }

  .bannerContainer {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
  }

  .flipped {
    transform: scaleX(-1);
  }

  .desktop-only {
    @media only screen and (max-width: 560px) {
      display: none;
    }
  }

  .gold-clear-button {
    font-family: athelas;
    background: none;
    color: $gold;
    border: solid $gold 1px;
    text-decoration: none;
    font-size: 20px;
    padding: 10px 20px;
    transition-duration: .5s;
    margin-bottom: 15px;
    cursor: pointer;
    &:hover {
      color: $dark-blue;
      background: $gold;
    }
  }

  .gold-link {
    color: $gold;
    font-size: 15px;
  }

  .fancy-button {
    background: $gold;
    box-shadow: 5px 5px 0px $blue;
    cursor: pointer;
    font-family: athelas;
    font-weight: bold;
    font-size: 20px;
    padding: 10px 20px;
    border: none;

    p {
      font-size: 14px;
      margin: 0px;
      font-weight: normal;
    }
  }

  /* AUTH STYLING */
  /*  Putting this here so i don't need to duplicate in  two components*/

  #auth-title {
    font-family: nandaka;
    font-size: 50px;
    color: $brown;
    margin: 0px;
    margin-bottom: -7px;
    padding-top: 10vh;
  }

  #auth-subtitle {
    font-size: 20px;
    // margin-bottom: 10px;
  }

  .auth-container {
    position: relative;
    z-index: 15;
    padding-top: 10px;
    background: $brown;
    width: 50vw;
    min-width: 300px;
    color: white;
    margin-left: 50%;
    transform: translatex(-50%);
  }

  .simple-text-input {
    font-family: athelas;
    background: none;
    border: none;
    border-bottom: 2px solid white;
    color: white;
    font-size: 16px;
    margin-bottom: 20px;
  }

  #auth-ground {
    background: $sand;
    width: 100vw;
    height: 15vh;
    position: absolute;
    bottom: 0px;
    z-index: 5;
  }

  #auth-cactus {
    height: 50vh;
    z-index: 10;
    position: absolute;
    bottom: 7vh;
    left: 10vw;
  }

  #auth-rocks {
    height: 7vh;
    z-index: 10;
    position: absolute;
    bottom: 7vh;
    left: 26vw;
  }

  @media only screen and (max-width: 850px) {
    #bannerL {
      display: flex;
      justify-content: space-between;
    }

    #bannerR {
      flex-direction: column;
    }

    #bannerR:not(.hidden) {
      display: none;
    }

    #banner {
      flex-direction: column;
    }

    #hamburgMenu {
      display: block;
      cursor: pointer;
    }

    #hamburgIcon {
      filter: invert(100%);
      width: 40px;
      height: 40px;
      padding: 5px;
    }

    #bannerLMobile {
      display: block;
    }

    .banner-link {
      margin-bottom: 0px;
      padding-bottom: 10px;
      text-align: left;
    }
  }
</style>
